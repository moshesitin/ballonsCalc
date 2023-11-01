    <script setup>
import { ref, defineProps, computed } from 'vue'

const props = defineProps({
  MathMenu: Array,
  WorkMenu: Array,
  GenMenu: Array,
  discountPercent: Number
})
const sumPrice = computed(() => {
  let sum = 0
  let Worksum = 0
  const calcObj = {}
  let profitInPrcnt = 0
  if (props.MathMenu) {
    for (let i = 0; i < props.MathMenu.length; i++) {
      sum += props.MathMenu[i].price * props.MathMenu[i].quantity
    }
  }
  if (props.WorkMenu) {
    for (let i = 0; i < props.WorkMenu.length; i++) {
      Worksum += props.WorkMenu[i].price * props.WorkMenu[i].quantity //Умножение часов работы на их стоимость
    }
  }
  if (props.GenMenu) {
    for (let i = 0; i < props.GenMenu.length; i++) {
      sum += props.GenMenu[i].price * props.GenMenu[i].quantity
    }
  }
  sum += Worksum
  profitInPrcnt = (Worksum / sum) * 100
  calcObj.sum = sum
  calcObj.Worksum = Worksum
  calcObj.profitInPrcnt = profitInPrcnt
  calcObj.profitAfterDiscountInNis = Worksum - (sum * (props.discountPercent/100))
  calcObj.profitAfterDiscountInPrcnt = (calcObj.profitAfterDiscountInNis / sum) * 100
  return calcObj
})
</script>
    
<template>
  <div class="sum-wrapper">
    <h2> {{`חלון סיכום ${props.GenMenu ? " " : "לא"} כולל עלויות כלליות`}} </h2>
    <div class="container">
      <div class="general-sum">
        {{ `סך הכל ליחידה :₪${sumPrice.sum}` }}
      </div>
      <div class="other-profits">
        <div>
          {{ `רווח באחוזים: %${sumPrice.profitInPrcnt ? sumPrice.profitInPrcnt.toFixed(2) : 0} ` }}
        </div>
        <div>
          {{ `רווח באחוזים אחרי הנחה: %${sumPrice.profitAfterDiscountInPrcnt ? sumPrice.profitAfterDiscountInPrcnt.toFixed(2) : 0} `}}
        </div>
      </div>
      <div class="other-profits">
        <div>
          {{ `רווח בש"ח: ₪${sumPrice.Worksum ? sumPrice.Worksum : 0} ` }}
        </div>
        <div>
          {{ ` רווח בש"ח אחרי הנחה: ₪${sumPrice.profitAfterDiscountInNis ? sumPrice.profitAfterDiscountInNis.toFixed(2) : 0}` }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sum-wrapper h2 {
  font-size: 30px;
  display: flex;
  justify-content: center;
}
.container {
  width: 100%;
  /* height: 200px; */
  background-color: #ff8888;
  display: flex;
  align-items: baseline;
  flex-direction: row-reverse;
  gap: 34px;
  padding: 25px;
}
.general-sum {
  font-size: 35px;
}
.other-profits {
  font-size: 25px;
}
</style>
