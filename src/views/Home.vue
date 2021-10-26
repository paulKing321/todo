<template>
  <div class="home">
    <h1 class="head">My Todo App</h1>
    <form @submit.prevent="addNewTodo">
      <label>New Todo</label>
      <input v-model="newTodo" name="newTodo">
      <button>Add New Todo</button>
    </form>
    <button @click="markAllDone">Mark All Done</button>
    <button @click="removeAllTodos">Remove All</button>
    <ul>
      <li class="todo" v-for="todo in todos" :key="todo.id">
        <h3 :class="{ done: todo.done}" @click="toggleDone(todo)">{{ todo.content }}</h3>
        <span>
          <button @click="removeTodo(index)">x</button>
        </span>
      </li>
    </ul>
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
.home {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
  background: linear-gradient(rgba(0,0,0,0.5), deeppink);
  /* align-items: center; */
  /* justify-content: center; */

}

.head {
  font-family: 'Kaushan Script', cursive;
  color: aliceblue;
}

input, button, textarea, p, div, section, article, select {
  display: block;
  width: 80%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
  /* align-items: center; */
  /* align-content: center; */
  /* justify-content: center; */
}
.done {
  text-decoration: line-through;
  color: grey;
}
.todo {
  cursor: pointer;
}
.x{
  display: flex;
  flex-direction: row;
}
</style>