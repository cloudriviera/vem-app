<template>
  <div class="app">
    <h1>Task Manager</h1>
    <TaskList />
  </div>
</template>

<script>
import TaskList from './components/TaskList.vue';

export default {
  name: 'App',
  components: {
    TaskList
  }
};
</script>