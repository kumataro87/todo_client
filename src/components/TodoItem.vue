<template>
  <div>
    <span :class="{ 'completed': todo.completed }">{{ todo.title }}</span>
    <button @click="deleteTodo">Delete</button>
    <button @click="toggleCompleted">Toggle Completed</button>
  </div>
</template>

<script>
export default {
  props: {
    todo: Object
  },
  methods: {
    deleteTodo() {
      // delete-todoイベントを発火し、todo.idを親コンポーネントに渡す
      this.$emit('delete-todo', this.todo.id);
    },
    toggleCompleted() {
      // update-todoイベントを発火し、todoオブジェクトを親コンポーネントへ渡す
      this.$emit('update-todo', {  ...this.todo, completed: !this.todo.completed });
    }
  }
}
</script>

<style>
.completed {
  text-decoration: line-through;
}

</style>