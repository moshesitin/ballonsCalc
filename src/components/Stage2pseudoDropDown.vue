    <script setup>
import { ref, reactive } from 'vue'

const isOpen = ref(false)
const selectedCategory = ref('')
const selectedItem = ref(null)


const items = reactive([
  { category: 'בלונים', isOpen: false, subCategory: [
    {name: 'בלוני לטקס', isOpen: false, large: []},
    {name: 'בלוני מיילר', isOpen: false, large: []},
    {name: `אקווה\בובו`, isOpen: false, large: []},
    {name: 'באבל', isOpen: false, large: []},
    {name: 'אורבז', isOpen: false, large: []},
  ] },
  { category: 'הליום', isOpen: false, subCategory: [
  {name: 'בלוני לטקס', isOpen: false, large: []},
    {name: 'בלוני מיילר', isOpen: false, large: []},
    {name: `אקווה\בובו`, isOpen: false, large: []},
    {name: 'באבל', isOpen: false, large: []},
    {name: 'אורבז', isOpen: false, large: []},
  ] },
  { category: 'ציוד', isOpen: false, subCategory: [
  {name: 'דבקים', isOpen: false, type: []},
  {name: `בדים\םסרטי`, isOpen: false, type: []},
  {name: `סטנדים\תקונסתרוקציו`, isOpen: false, type: []},
  {name: `שונות`, isOpen: false, type: []},
  ] },
  { category: 'שעות עבודה', isOpen: false, subCategory: [
    'עבודה בסיסית',
    'עבודה אמנותית',
    'עבודה מורכבת'
  ] },
  { category: 'עלויות כלליות', isOpen: false, subCategory: [
    'זמן עבודה כללי',
    'משלוח',
    'עובדים',
    'שונות',
  ] }
])

const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const toggleItem = (index) => {
  items[index].isOpen = !items[index].isOpen
  selectedItem.value = items[index]

  for (let i = 0; i < items.length; i++) {
    if (i !== index) {
      items[i].isOpen = false
    }
  }

  // if (items[index].isOpen && items[index].subCategory.length === 0) {
  //   items[index].subCategory = generateSubCategory()
  // }
}

// const generateSubCategory = () => {
//   const subCategory = []
//   for (let i = 1; i <= 5; i++) {
//     subCategory.push({ text: `Дополнительный элемент ${i}` })
//   }
//   return subCategory
// }
</script>
    
<template>
  <div class="stage2">
    <h2>שלב 2 בחר חומרים</h2>
    <button class="category-btn" @click="toggleDropdown">{{ 'קטגוריה' }}</button>
    <div class="categoty-content" v-show="isOpen">
      <div class="category-wrapper" v-for="(item, index) in items" :key="index">
        <div class="category-item" @click="toggleItem(index)">
          <div :class="{ 'selected-item': selectedItem === item }">
            {{ item.category }}
          </div>
        </div>
        <div v-show="item.isOpen" class="additional-content">
          <div
            class="subCategory"
            v-for="(additionalItem, additionalIndex) in item.subCategory"
            :key="additionalIndex"
          >
            {{ additionalItem.text }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.category-btn {
  padding: 5px;
  border: 1px solid #433333;
  background-color: #e48389;
  color: #e32e2e; 
  border-radius: 5px;
  padding: 5px;
  font-size: 18px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.category-content {
  margin-top: 10px;
}

.category-wrapper {
  display: flex; 
  flex-direction: row-reverse;
  cursor: pointer;
}
.selected-item {
  border: 1px solid #433333;
  background-color: #e48389;
  color: #e32e2e; 
  border-radius: 5px;
  cursor: pointer;
  padding: 5px;
}



.subCategory {
  padding: 5px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  cursor: pointer;
}
</style>


