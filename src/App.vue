<template>
  <div id="app">
    <Header />
    <button @click="created">Load from API</button>
    <AddTodo v-on:add-todo="AddTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"></Todos>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';

export default {
  name: 'app',
  components: {
    Todos, Header, AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    AddTodo(newTodo){      
      this.todos = [...this.todos, newTodo];
    },
    created() {      
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(json => this.todos = json)
    }
  }
}
</script>

<style>

</style>
