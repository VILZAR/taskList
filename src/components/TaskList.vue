<template>
  <div>
    <h1>Task List</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.done" @change="updateTasks" />
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: []
    };
  },
  created() {
    this.fetchTask();
  },
  methods: {
    async fetchTask() {
      const response = await fetch('/tasks.json');
      const data = await response.json();
      this.tasks = data;

      const savedTasks = localStorage.getItem('tasks');
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    },
    updateTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  }
};
</script>

<style scoped>
ul {
  list-style-type: none;
  margin: auto;
  border: 1px solid black;
  width: max-content;
  height: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  padding: 20px;
}
li {
  margin: 15px 0;
}
</style>