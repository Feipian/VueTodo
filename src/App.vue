<template>
  <main>
    <header>
      <img src="./assets/todo-logo.svg" alt="todo-logo">
      <h1>Hello Todo World</h1>
    </header>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'"> All tasks </button>
      <button @click="filter = 'favs'"> Favorite </button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="loading">Loading tasks...</div> 
    
    <!-- new Task form -->
    <div class="new-task-form">
      <TaskForm></TaskForm>
    </div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p> All task </p>
      <p>You have {{ totalCount }} task left to do</p>
      <div v-for="task in tasks" :key="task.id" >
        <TaskDetails :task="task"></TaskDetails>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>Favorite tasks</p>
      <p>You have {{ favCount }}  task favorite</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetails :task="task"></TaskDetails>
      </div>
    </div>

    <button class="reset-button" @click="TaskStore.$reset">reset state</button>

  </main>
</template>

<script>
  import { ref } from 'vue';
  import { useTaskStore } from '../stores/TaskStore';
  import TaskDetails from './components/TaskDetails.vue'
  import TaskForm from './components/TaskForm.vue'
import { storeToRefs } from 'pinia';

  
  export default {
    components: {
      TaskDetails,
        TaskForm,
    },

    setup(){
      const TaskStore = useTaskStore()
      
      const { tasks, loading, favs, totalCount, favCount} = storeToRefs(TaskStore)
      // fetch tasks
      TaskStore.getTasks()
      const filter = ref('all')

      return { TaskStore, filter, tasks, loading, favs, totalCount, favCount}

    }
  }
</script>