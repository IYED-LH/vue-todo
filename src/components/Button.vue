<template>
<button @click="$emit('show-task-form')" :style="{ background: color }" class="btn">{{ text }}</button>
</template>

<script>
export default  {
  name: 'Button',
  props: {
    text: String,
    color: String,
    },
    
  }

</script>