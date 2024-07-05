<template>
	<div :class="`task ${task.done ? 'is-complete' : ''}`">
	  <div class="content" v-if="!isEditing">{{ task.content }}</div>
	  <input v-else type="text" v-model="updatedContent" @keypress.enter="updateTask" @blur="updateTask" />
  
	  <div class="buttons">
		<button @click="toggleDone">{{ task.done ? 'Undo' : 'Done' }}</button>
		<button @click="startEditing" v-if="!isEditing">Edit</button>
		<button @click="updateTask" v-if="isEditing">Update</button>
		<button @click="removeTask" class="delete">Delete</button>
	  </div>
	</div>
  </template>
  
  <script>
  export default {
	props: ['task'],
	data() {
	  return {
		isEditing: false,
		updatedContent: this.task.content
	  };
	},
	methods: {
	  toggleDone() {
		this.$store.commit('TOGGLE_TASK', this.task);
	  },
	  removeTask() {
		this.$store.commit('REMOVE_TASK', this.task);
	  },
	  startEditing() {
		this.isEditing = true;
	  },
	  updateTask() {
		if (this.isEditing) {
		  this.$store.commit('UPDATE_TASK', { task: this.task, content: this.updatedContent });
		  this.isEditing = false;
		}
	  }
	}
  };
  </script>
  
  <style>
  /* Add your styles here */
  </style>
  