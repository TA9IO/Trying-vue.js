<template>
  <form @submit.prevent="addNewTodo">
  <h1 class='title'>Vue Todo App</h1>
    <label class='label'>
      New Todo
      <input class="input" v-model="todo" type="text" />
    </label>
    <button class="add-button-hover bn" type="submit">Add Todo</button>
  </form>
  <ul class='todos-container'>
    <li v-for="todo in todos" :key="todo.key" class='todo-li'>
      <h3
        @click="togleDone(todo)"
        class="todo"
        :class="todo.done ? 'done' : 'notdone'"
      >
        {{ todo.what }}
        
      </h3>
      
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    let todo = ref("");
    let todos = ref([]);
    const addNewTodo = (e) => {
      e.preventDefault();
      todos.value.push({
        key: Math.random().toString(32),
        done: false,
        what: todo.value,
      });
      todo.value = "";
      console.log(todos.value);
    };
    const togleDone = (todo) => {
      todo.done = !todo.done;
    };

    return {
      addNewTodo,
      todo,
      todos,
      togleDone,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.title::first-letter {
  color: #3FB27F
}
li {
  list-style: none;
}
.label {
  font-size: 1.5rem
}
.todos-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  min-width: 100%;
  row-gap: 5px;
  padding: 0
}
.todo-li {
  width: 70%;
}
.todo {
  box-shadow: 1px 1px 20px 1px rgba(0, 0, 0, 0.2);
  border-radius: 15px;
  padding: 5px;
  cursor: pointer;
  user-select: none;
  width: 100%;
}
.done {
  text-decoration: line-through;
  color: red;
  cursor: pointer;
}
.input {
  height: 2.5rem;
  border-radius: 1rem;
  font-size: 1rem;
  font-weight: bold;
  border: 2px solid #3FB27F;
  padding-left: 1rem;
}
.input:focus {
  border: 2px solid #5ad69f;
  outline: none
}
.add-button-hover {
  width: 10em;
  font-size: 1rem;
  font-weight: 600;
  color: #fff;
  cursor: pointer;
  margin: 20px;
  height: 3rem;
  text-align: center;
  border: none;
  background-size: 300% 100%;
  border-radius: 50px;
  moz-transition: all 0.4s ease-in-out;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}

.add-button-hover:hover {
  background-position: 100% 0;
  moz-transition: all 0.4s ease-in-out;
  -o-transition: all 0.4s ease-in-out;
  -webkit-transition: all 0.4s ease-in-out;
  transition: all 0.4s ease-in-out;
}

.add-button-hover:focus {
  outline: none;
}

.add-button-hover.bn {
  background-image: linear-gradient(
    to right,
    #3FB27F,
    #5ad69f,
    #04befe,
    #3f86ed
  );
  box-shadow: 0 4px 15px 0 rgba(65, 132, 234, 0.75);
}
</style>
