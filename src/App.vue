<template>
  <div class="container">
    <h1>ToDo List</h1>
    <md-field>
      <md-input
        v-model="currentTodo"
        @keydown.enter="addTodo()"
        placeholder="Click here to add an item to your ToDo List"
      ></md-input>
    </md-field>
    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <input class="completeButton" type="checkbox" v-model="todo.completed" />
        <span
          class="todo-item-label"
          :class="{completed: todo.completed}"
          @dblclick="editTodo(todo)"
          v-if="!todo.edit"
        >{{todo.label}}</span>
        <md-input
          v-else
          class="todo-item-edit"
          type="text"
          v-model="todo.label"
          @keyup.enter="completedEdit(todo)"
        ></md-input>
        <md-raised class="closeButton" @click="removeTodo(todo)">Delete</md-raised>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        edit: false
      });
      this.currentTodo = "";
    },
    editTodo(todo) {
      todo.edit = true;
    },
    completedEdit(todo) {
      todo.edit = false;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style>
.container {
  background-color: #1f2833;
  color: #66fcf1;
  text-align: center;
}
li {
  list-style: none;
}
.completed {
  text-decoration: line-through;
}
.closeButton {
  float: right;
}
.closeButton:hover {
  cursor: pointer;
  color: red;
}
.todo-item-label:hover {
  cursor: grab;
}
</style>