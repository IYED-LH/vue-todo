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

    addTask(task) {
      this.tasks.push(task)
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
        return task
      })
    }
 },

  created() {
    this.tasks = [
      {
        id: 1,
        title: 'Task 1',
        date: '01/01/2020',
        completed: true
      },
      {
        id: 2,
        title: 'Task 2',
        date: '01/01/2020',
        completed: false
      },
      {
        id: 3,
        title: 'Task 3',
        date: '01/01/2020',
        completed: true
      }
    ]
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
