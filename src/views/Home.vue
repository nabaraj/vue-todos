<template>
  <div id="app">
    <Addtodo v-on:add-todo="addTodo" v-bind:isLoading="loading" />
    <Todo v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todo from "./../components/Todos";
import Addtodo from "./../components/Addtodo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todo,

    Addtodo
  },
  data() {
    return {
      todos: [],
      loading: false
    };
  },
  methods: {
    deleteTodo(id) {
      //
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          console.log(res.data);
          this.todos = this.todos.filter(todo => todo.id !== id);
        })
        .catch(err => console.log(err));
    },
    addTodo({ title, completed }) {
      // this.todos = [newTodo, ...this.todos];
      this.loading = true;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => {
          this.loading = false;
          return (this.todos = [res.data, ...this.todos]);
        })
        .catch(err => console.log(err));
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));

    // https://jsonplaceholder.typicode.com/todos
    console.log("created");
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
