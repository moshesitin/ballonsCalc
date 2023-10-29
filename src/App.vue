<script setup>
import { ref, toRefs } from 'vue'
import Stage1 from './components/Stage1.vue'
// import Stage2pseudoDropDown from './components/Stage2pseudoDropDown.vue'
import Stage2copy from './components/Stage2copy.vue'
import Stage3 from './components/Stage3.vue'
import Stage4 from './components/Stage4.vue'
import commonSum from './components/commonSum.vue'

const menu = ref(null)

const updateMenu = (newMenu) => {
  menu.value = newMenu
}
</script>

<template>
  <div
    class="wrapper p-3 text-primary-emphasis bg-primary-subtle border border-primary-subtle rounded-3"
  >
    <h1>מחשבון תמכור</h1>
    <Stage1 />
    <Stage2copy @update-menu="updateMenu" />
    <Stage3 />
    <Stage4 />
    <commonSum :menu="menu" />
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
