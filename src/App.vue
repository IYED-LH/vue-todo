<template>
<div class="container">

<Header :toggleAddTask="showAddTask" @show-task-form="showTaskForm" />

<div v-show="showAddTask">
<AddTask @add-task="addTask" />
</div>

<Tasks @completed="completedTask"  @delete="deleteTask" :tasks="tasks"/>

</div>
</template>

<script>
const axios = require('axios').default;
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,          
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },

  methods: {


    showTaskForm() {
      this.showAddTask = !this.showAddTask;
    },

    

    async addTask(task) {
      const response = await axios.post ('http://localhost:5000/tasks',task); 
      this.tasks.unshift(response.data);
      },

    deleteTask(id) {
      if (confirm('Are you sure you want to delete this task?'))
      {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
   },
 
    completedTask(id) {
      this.tasks = this.tasks.map((task) => { (task.id === id) ?  
        task.completed = !task.completed : ''
        return task })
    },

    async fetchtasks() { 
      const response =  await fetch('http://localhost:5000/tasks')
      const data = await response.json()
      
      return data

    },
    
    async fetchtask(id) { 
      const response =  await fetch('http://localhost:5000/tasks/'+id)
      const data = await response.json()
      
      return data

    } ,
 },

  async created() {
    this.tasks = await this.fetchtasks()
  },
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  width: 25%;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 14px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
