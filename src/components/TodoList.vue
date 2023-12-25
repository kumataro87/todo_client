<template>
  <div>
    <add-todo @add-todo="addTodo" />
    <todo-item
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
    />
  </div>
</template>

<script>
import axios from 'axios';
import TodoItem from './TodoItem.vue';
import AddTodo from './AddTodo.vue';

export default {
  components: {
    TodoItem,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  created() {
    this.fetchTodos();
  },
  methods: {
    fetchTodos() {
      axios.get(`${process.env.VUE_APP_API_URL}/todos`)
        .then(response => {
          this.todos = response.data;
        });
    },
    addTodo(newTodo) {
      axios.post(`${process.env.VUE_APP_API_URL}/todos`, newTodo)
        .then(response => {
          this.todos.push(response.data);
        });
    },
    deleteTodo(todoId) {
      axios.delete(`${process.env.VUE_APP_API_URL}/todos/${todoId}`)
        .then(() => {
          this.todos = this.todos.filter(todo => todo.id !== todoId);
        });
    },
    updateTodo(updatedTodo) {
      console.log(updatedTodo)
      axios.put(`${process.env.VUE_APP_API_URL}/todos/${updatedTodo.id}`, updatedTodo)
        .then(response => {
          const index = this.todos.findIndex(todo => todo.id === response.data.id);
          this.todos.splice(index, 1, response.data);
        });
    }
  }
};
</script>
