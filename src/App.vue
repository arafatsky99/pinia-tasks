<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="">
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">

      <TaskForm />
    </div>

    <nav class="filter">
      <button v-on:click="taskfilter='all'">All</button>
      <button v-on:click="taskfilter='favs'">Favs</button>
    </nav>
    
    <div class="loading" v-if="loading">Loading Tasks...</div>
    <div class="task-list" v-if="taskfilter=='all'">
      <p>You have {{ totalCount }} task left to do</p>
      <div v-for="task in tasks" :key="tasks.id">
        
        <TaskDetails :task="task" />

      </div>
    </div>


    <div class="task-list" v-if="taskfilter=='favs'">
      <p>You have {{ favCount }} fav task left to do</p>
      <div v-for="task in favs" :key="favs.id">
        
        <TaskDetails :task="task" />

      </div>
    </div>

    <button @click="taskStore.$reset">reset</button>

  </main>
</template>

<script>
  import { useTaskStore } from './stores/TaskStore';
  import TaskDetails from './components/TaskDetails.vue';
  import { ref } from 'vue';
  import TaskForm from './components/TaskForm.vue';
  import {storeToRefs} from 'pinia'

  export default {
    components: {
    TaskDetails,
    TaskForm
},
    setup() {

      const taskfilter = ref('all');

      const taskStore = useTaskStore()



      taskStore.getTasks()

      const {tasks,loading,favs,favCount,totalCount} = storeToRefs(taskStore)

      return {taskStore, taskfilter, tasks,loading,favs,favCount,totalCount};
    }
  }
</script>