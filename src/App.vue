<script setup>
import Stage1 from './components/Stage1.vue'
import Stage2 from './components/Stage2.vue'
import Stage2copy from './components/Stage2copy.vue'
// import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <div class="wrapper p-3 text-primary-emphasis bg-primary-subtle border border-primary-subtle rounded-3">
      <h1>מחשבון תמכור</h1>
      <Stage1 />
      <!-- <Stage2 /> -->
      <Stage2copy />
    </div>
</template>

<style scoped>
.wrapper{
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
