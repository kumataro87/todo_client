<template>
  <div>
    <input v-model='newTodoTitle' placeholder="新しいタスクを追加する" />
    <button @click="addTodo">追加</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoTitle: ''
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoTitle.trim()) {
        this.$emit('add-todo', { title: this.newTodoTitle, completed: false });
        this.newTodoTitle = '';
      }
    }
  }
}
</script>

<style>

</style>