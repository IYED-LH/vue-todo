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
      this.tasks.push(response.data);
      },

    async deleteTask(id) {
      if (confirm('Are you sure you want to delete this task?'))
      {
      await axios.delete ('http://localhost:5000/tasks/'+id);
      this.tasks = this.tasks.filter(task => task.id !== id);
      }
      
    },
  
 
   async completedTask(id) {
      
      const taskToToggle = await this.fetchTask(id)
      const updTask = { ...taskToToggle, completed: !taskToToggle.completed }
      const response = await axios.put (`http://localhost:5000/tasks/${id}`, updTask);
      
      const data = response.data;
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, completed: data.completed } : task
      )
    },

    async fetchTasks() { 
      
      const response =  await axios.get ('http://localhost:5000/tasks/')
      const data = response.data;

      return data
    },
    
    async fetchTask(id) { 
      const response =  await axios.get ('http://localhost:5000/tasks/'+id)
      const data = response.data;
      return data

    } ,
 },

  async created() {
    this.tasks = await this.fetchTasks()
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
