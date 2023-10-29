    <script setup>
import { ref, defineProps, computed } from 'vue'

const props = defineProps({
  menu: Array
})
const sumPrice = computed(() => {
  let sum = 0;
  if (props.menu) {
    for (let i = 0; i < props.menu.length; i++) {
      sum += props.menu[i].price
    }
  }
  return sum;
})
</script>
    
<template>
  <div class="sumwrapper">
    <div>{{`סך הכל ליחידה (לא כולל עלויות כלליות):
₪${sumPrice}`}}</div>
   <div></div>
    <div></div>
  </div>
</template>

<style scoped>
.sumwrapper{
  width: 100%;
  height: 200px;
  font-size: 35px;
  background-color: #ff8888;
}
</style>
