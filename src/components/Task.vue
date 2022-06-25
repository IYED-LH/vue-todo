<template>
<div @dblclick="$emit('completed',(task.id))"  :class= "[task.completed ? 'done' : 'undone', 'task']">

<h3>{{task.title}} 
<i  @click="$emit('delete', (task.id))" class="fas fa-times"></i>
</h3>

<p>{{task.date}}</p>

</div>
</template>

<script>

export default {
  name: 'Task',
  props: {
      task: Object,
    }, 
  }

</script>

<style scoped>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.done {
  border-left: 5px solid green;
}

.undone {
  border-left: 5px solid rgb(255, 179, 0);
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  }

</style>