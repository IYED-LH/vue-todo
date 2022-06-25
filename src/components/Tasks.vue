<template>
<div :key="task.id"  v-for="task in tasks" >
  
  <Task @completed="$emit('completed', (task.id))"  @delete="$emit('delete', task.id)" :task="task" /> 

</div>
</template>

<script>
import Task from './Task.vue'
export default{
    name: 'Tasks',
    props: {
        tasks: Array
    },
    components: {
        Task,
    },
    emits: ['delete'],
}
</script>

