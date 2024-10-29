<template>
  <div class="task-list">
    <div class="add-task">
      <input v-model="newTask" placeholder="New task..." @keyup.enter="addTask">
      <button @click="addTask">Add Task</button>
    </div>
    <ul>
      <li v-for="task in tasks" :key="task._id">
        {{ task.title }}
        <button @click="deleteTask(task._id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TaskList',
  data() {
    return {
      tasks: [],
      newTask: ''
    };
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await axios.get('/api/tasks');
        this.tasks = response.data;
      } catch (error) {
        console.error('Error fetching tasks:', error);
      }
    },
    async addTask() {
      if (!this.newTask.trim()) return;
      try {
        await axios.post('/api/tasks', { title: this.newTask });
        this.newTask = '';
        await this.fetchTasks();
      } catch (error) {
        console.error('Error adding task:', error);
      }
    },
    async deleteTask(id) {
      try {
        await axios.delete(`/api/tasks/${id}`);
        await this.fetchTasks();
      } catch (error) {
        console.error('Error deleting task:', error);
      }
    }
  }
};
</script>