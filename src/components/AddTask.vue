<template>
  <form @submit.prevent="onSubmit" class="form">
    <a-input v-model:value="title" class="form__input" type="text" placeholder="Create task" />
    <a-button htmlType="submit" type="primary" ghost>Create</a-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ""
    }
  },

  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTask = {
          id: Date.now(),
          title: this.title,
          completed: false
        }

        this.$emit("add-task", newTask)
        this.title = ""
      }
    }
  }
}
</script>

<style scoped>
.form {
  display: flex;
  align-items: center;
  max-width: 400px;
  margin: 0 auto;
}
</style>