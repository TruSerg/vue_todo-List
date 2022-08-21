<template>
  <div class="tasks__body">
    <ul>
      <TaskItem
          v-for="(task, index) of tasks"
          v-bind:task="task"
          v-bind:index="index"
          v-on:remove-task="removeTask"
      />
    </ul>
  </div>
</template>

<script>
import TaskItem from "@/components/TaskItem"

export default {
  props: ["tasks"],

  methods: {
    removeTask(id) {
        this.$emit('remove-task', id)
    }
  },

  components: {
    TaskItem
  },
}
</script>

<style scoped>
.tasks__body {
  margin-top: 2rem;
}
</style>

