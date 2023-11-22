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
      <div class="other-profits-wrapper">
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
  </div>
</template>

<style scoped>

.sum-wrapper {
  width: 100%;
  max-width: 800px;
  background-color: #fffee1;
  /* margin-bottom: 20px; */
  border: 2px solid #93916e;
  border-radius: 10px;
  padding: 20px;
  margin: 20px auto;
}

.sum-wrapper h2 {
  font-size: 18px;
  display: flex;
  justify-content: center;
  text-align: center;
  color: #37474f;
  /* font-weight: bold; */
  /* margin-top: 20px; */
  font-family: 'Montserrat-Medium',Arial,sans-serif;
  /* border: 1px 0 0 0 dotted grey; */
}

.container {
  width: 100%;
  /* background-color: #ff8888; */
  display: flex;
  flex-direction: column;
  align-items: center;
  /* flex-direction: row-reverse; */
  gap: 20px;
  border-radius: 10px;
  /* padding: 20px; */
  direction: rtl;
}

.general-sum {
  font-size: 26px;
  font-weight: bold;
}

.other-profits-wrapper {
  display: flex;
  justify-content: space-evenly;
  width: 100%;
}
.other-profits {
  font-size: 18px;
}

@media (max-width: 1024px) {
.other-profits {
  font-size: 12px;
}
.other-profits-wrapper {
  flex-direction: column;
  padding-right: 50px;
}
} 

</style>
