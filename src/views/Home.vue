<template>
  <div class="todos">
    <h1 class="head">My Todo App</h1>
    <form class="flex" @submit.prevent="addNewTodo">
      <!-- <label>New Todo</label> -->
      <input placeholder="Input New Todo" v-model="newTodo" name="newTodo">
      <button class="add">Add</button>
    </form>
    <button class="button1" @click="markAllDone">Mark All Done</button>
    <button class="button2" @click="removeAllTodos">Remove All</button>
    <div>
      <div class="todo" v-for="todo in todos" :key="todo.id">
        <div>
          <button class="new" :class="{ done: todo.done}" @click="toggleDone(todo)">{{ todo.content }}</button>
          <button class="delete" @click="removeTodo(index)">x</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'Home',
  setup() {
    // i'm using refs this time around, and i need to use .value
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        done: false,
        content: newTodo.value,
      });
      newTodo.value =  '';
    }

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
.delete {
  color: red;
  border: cadetblue 2px solid;
  background: cadetblue;
  padding: 0px 0px;
  border-radius: 0;
  font-size: 20px;
  margin-left: 80px;
}
</style>