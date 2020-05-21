<template>
  <div class="todoItem" v-bind:class="{isCompleted:todo.completed}">
    <p>
      <label :for="'check-'+todo.id">
        <input
          type="checkBox"
          :id="'check-'+todo.id"
          v-on:change="toggleTodo"
          :checked="todo.completed"
        />
        {{todo.title}}
      </label>
      <button class="del" @click="$emit('del-todo',todo.id)">X</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    toggleTodo() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todoItem {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.isCompleted {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>