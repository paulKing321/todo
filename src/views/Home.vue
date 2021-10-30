<template>
  <div class="todos">
    <Toast v-if="showToast" />
    <Todos v-if="triggerToast" />
    <h1 class="head">My Todo App</h1>
    <form class="flex" @submit.prevent="addNewTodo">
      <!-- <label>New Todo</label> -->
      <input placeholder="Input New Todo" v-model="newTodo" name="newTodo">
      <button class="add" @click="triggerToast(newTodo.value)"> Add</button>
    </form>
    <button class="button1" @click="markAllDone">Mark All Done</button>
    <button class="button2" @click="removeAllTodos">Remove All</button>
    <div v-if="todos.length">
      <div class="todo" v-for="todo in todos" :key="todo.id">
        <!-- <div class="flex"> -->
          <transition name="new">
              <button class="new" :class="{ done: todo.done}" @click="toggleDone(todo)">{{ todo.content }}</button>
          </transition>
              <button class="delete" @click="removeTodo(index)">x</button>
        <!-- </div> -->
      </div>
    </div>

  </div>
</template>

<script>
import { ref } from 'vue';
import Toast from '../components/Toast';

export default {
  name: 'Home',
  components: {
    Toast
  },


  setup() {
    // i'm using refs this time around, and i need to use .value
    const showToast = ref(false)

    function triggerToast() {
      if (newTodo.value.length < 1) {
      showToast.value = true
      setTimeout(() => showToast.value = false, 3000)
      } else {
        showToast.value = false;
      }
    }

    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value,
        });
        newTodo.value =  '';
      } else {
        return triggerToast
      }
    }
    // const addNewTodo = () => {
    //   if (newTodo.value) {
    //     const id = Math.random()
    //     todos.value = [{ text: newTodo.value, id }, ...todos.value]
    //     newTodo.value = ''
    //   } else {
    //     this.$emit ('badValue');
    //   }
    // }    

    // function changeTodo() {
    //   if (newTodo.value.length = 0);
    //     return {
    //       triggerToast
    //     }
    //     else {
    //       return {
    //         addNewTodo()
    //       }
    //     }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true);
    }

    function removeAllTodos() {
      todos.value = [];
      //could also use this  'todos.value.length = 0;'
    }

    return {
      showToast,
      triggerToast,
      // changeTodo,
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,

    };
  }
}
</script>

<style>
todos {
  max-width: 400px;
  margin: 20px auto;
  position: relative;
}
input {
  font-style: italic;
  width: 80%;
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 10px;
  box-sizing: border-box;
  margin-bottom: 20px;
  margin-right: 30px;
}
.todos ul {
  position: relative;
  padding: 0;
}
.todos li {
  list-style-type: none;
  display: block;
  margin-bottom: 10px;
  padding: 10px;
  background: white;
  box-shadow: 1px 3px 5px rgba(0,0,0,1);
  border-radius: 10px;
  width: 100%;
  box-sizing: border-box;
}
.head {
  font-family: 'Kaushan Script';
  font-size: 50px;
}
.done {
  text-decoration: line-through;
  text-decoration-color: #fd068e;
  color: black;
}
button {
  color: white;
  background: black;
  border: 2px 2px 0 0;
  border-top-color: cornsilk;
  padding: 10px 5px 10px 5px;
  border-radius: 10px 0 10px 0;
}
.add{
  text-shadow: 0 0 0.125em hsl(0 0% 100% / 0.3), 0 0 0.45em currentColor;
  box-shadow: inset 0 0 0.5em 0 white, 0 0 0.5em 0 white;
  position: relative;

  /* transition: background-color 100ms linear; */
}
.add::before {
  pointer-events: none;
  /* pointer-events deactivates the hover and the focus to only work when the cursor is on the button not on the shadow  */
  content: "";
  position: absolute;
  background: white;
  top: 120%;
  left: 0;
  width: 100%;
  height: 100%;

  transform: perspective(1em) rotateX(40deg) scale(1, 0.35);
  filter: blur(1em);
  opacity: 0.7;
}
.add::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  box-shadow: 0 0 2em 0.5em white;
  opacity: 0;
  background-color: white;
  z-index: -1;
  transition: opacity 100ms linear;
}

.add:hover, .add:focus {
  background: #fd068e;
  color: var(--clr-background);
  text-shadow: none;
  font-family: 'Kaushan Script';
  font-weight: bold;
  transition: all 0.5s ease;
}

.add:hover::before,
.add:focus::before {
  opacity: 1;
}

.add:hover::after,
.add:focus::after {
  opacity: 1;
}

.button1, .button2 {
  letter-spacing: 2px;
  word-spacing: 8px;
  border-right: #fd068e solid;
  margin-top: 8px;
  padding: 10px 50px;
}
.button1 {
  margin-right: 210px;
}
.button2 {
  margin-right: 80px;
}
.new {
  margin-top: 50px;
  padding: 10px 100px;
  background: white;
  color: cadetblue;
  font-size: 15px;
  font-weight: bolder;
  font-family: serif;
  border-color: white;
  margin-left: 30px;
  min-width: 500px;
  max-width: 500px;
  box-shadow: 1px 3px 5px white;
}
/* .new-enter-from{
  opacity: 0;
  transform: translateY(-60px)
}
.new-enter-to{
  opacity: 1;
  transform: translateY(0);
} */
.new-enter-active{
  /* transition: all 0.3s ease; */
  animation: wobble 0.5s ease;
}

.new-leave-from{
  opacity: 1;
  transform: translateY(0)
}
.new-leave-to{
  opacity: 0;
  transform: translateY(-60px);
}
.new-leave-active{
  transition: all 0.3s ease;
}

@keyframes wobble {
  0% { transform: translateY(-60px); opacity: 0; }
  50% { transform: translateY(0px); opacity: 1; }
  60% { transform: translateX(8px) }
  70% { transform: translateX(-8px) }
  80% { transform: translateX(4px) }
  90% { transform: translateX(-4px) }
  100% { transform: translateX(0px) }
}

.delete {
  color: red;
  border: cadetblue 2px solid;
  background: cadetblue;
  padding: 0px 0px;
  border-radius: 0;
  font-size: 20px;
  margin-left: 80px;
}

@media screen and (max-width: 770px) {
  .todos {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 80%;
    margin: auto ;
    margin-top: -30px;
  }
  .button1, .button2 {
    width: 60vw;
    margin-top: 20px;
  }

  .new {
    min-width: 100%;
    width: 80%;
    margin: auto;
    margin-top: 20px;
  }
  .flex {
    display: flex;
    flex-direction: row;
  }
  .delete {
    display: none;
  }
  .add::before, add::after, add:hover::before, add:hover::after, add:focus::before, add:focus::after {
    display: none;
  }
}
</style>