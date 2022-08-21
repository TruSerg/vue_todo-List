<template>
    <Header />
  <div class="main__wrapper">
    <h2 class="tasks__title">Day's tasks</h2>
    <AddTask
      @add-task="addTask"
    />
    <div class="tasks__filter">
      <span class="tasks__filter-title">Filter</span>
      <a-select v-model:value="filter" class="tasks__select">
        <a-select-option value="all">All</a-select-option>
        <a-select-option value="completed">Completed</a-select-option>
        <a-select-option value="not-completed">Not completed</a-select-option>
      </a-select>
    </div>
    <TaskList
        v-if="filteredTasks.length"
        v-bind:tasks="filteredTasks"
        v-on:remove-task="removeTask"
    />
    <p v-else class="task__empty-text">No tasks!</p>
  </div>

</template>

<script>
import Header from "@/components/Header"
import TaskList from "@/components/TaskList"
import AddTask from "@/components/AddTask"

export default {
  name: 'App',

  data() {
    return {
      tasks: [],
      filter: "all"
    }
  },

  methods: {
    removeTask(id) {
       this.tasks = this.tasks.filter(task => task.id !== id)
    },

    addTask(task) {
      this.tasks.push(task)
    }
  },

 computed: {
   filteredTasks() {
     if (this.filter === "all") {
       return this.tasks
     }

     if (this.filter === "completed") {
       return this.tasks.filter(task => task.completed)
     }

     if (this.filter === "not-completed") {
       return this.tasks.filter(task => !task.completed)
     }
   }
 },

  components: {
    Header,
    TaskList,
    AddTask
  }
}
</script>

<style>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

body {
  max-width: 100%;
  margin: 0 auto;
}

.main__wrapper {
  padding: 20px 15px;
  min-height: 100vh;
  background-color: #FFDEAD;
}

.tasks__title {
  font-size: 28px;
  margin-bottom: 2rem;
  color: #2690fe;
}

.tasks__filter {
  margin-top: 2rem;
}

.tasks__filter-title {
  font-size: 20px;
  color: #2690fe;
  margin-right: 1rem;
}

.tasks__select {
  display: block;
  width: 150px;
}

.task__empty-text {
  margin-top: 5rem;
  font-size: 25px;
  color: rgb(101, 101, 101);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #FFDEAD;
}
</style>
