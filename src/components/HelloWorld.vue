<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
    <h4>{{ msg }} fait du VueJS</h4>  
</template>

<style scoped>
</style>
