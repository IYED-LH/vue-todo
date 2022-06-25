<template>
<header>
    <h1>Task Tracker</h1>
    <Button @show-task-form="$emit('show-task-form')" :text="toggleAddTask ? 'Close' : 'Add Task'" :color="toggleAddTask ? 'rgb(231, 36, 36)' : 'green'"/>
</header>
</template>

<script>
import Button from './Button.vue'
export default {
    name: 'Header',
    props: {
        toggleAddTask: {
            type: Boolean,
            default: false
        }
    },
    components: { 
        Button 
    
    }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  
}
</style>