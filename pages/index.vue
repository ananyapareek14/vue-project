<template>
  <main>
    <h1>Task Manager</h1>
    <p>Create a list of tasks</p>

    <div class="create-new">
      <input 
        type="text" 
        v-model="newTask" 
        placeholder="Add a new task" 
        @keypress.enter="addTask" />
      <button @click="addTask">Add</button>
    </div>

    <div class="tasks">
      <Task
        v-for="(task, i) in $store.state.tasks"
        :key="i"
        :task="task" />
    </div>

  </main>
</template>

<script>
import Task from '~/components/Task.vue';

export default {
  components: {
    Task
  },
  data() {
    return {
      newTask: ''
    };
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.$store.commit('ADD_TASK', this.newTask);
        this.newTask = '';
      }
    }
  }
};
</script>

<style>
/* Add your styles here */
</style>
