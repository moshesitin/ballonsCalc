    <script setup>
import { ref, reactive, defineEmits } from 'vue'
const selectedType = ref(null)
const quantity = ref(0)
const price = ref(0)
const selectedMenus = reactive([])

const emit = defineEmits(['update-menu'])

const filters = reactive([
      { name: 'זמן עבודה כללי' },
      { name: 'משלוח' },
      { name: 'עובדים' },
      { name: 'שונות' }
])

const addNewMenu = () => {
  // create info for menu
    const menu = {
      type: selectedType.value,
      quantity: quantity.value,
      price: price.value
    }
    selectedMenus.push(menu)
    quantity.value = 0
    price.value = 0
}

emit('update-menu', selectedMenus)
</script>
    
<template>
  <div class="calc-stage calc-stage4">
    <h2>שלב 4 עלויות כלליות</h2>
     <div class="strawberry-pink-bg-wrapper">
        <div class="strawberry-pink-bg-select-wrapper">
          <select
            v-model="selectedType"
            @change="addNewMenu"
            class="strawberry-pink-bg"
          >
            <option disabled value="" class="rose-red-text">בחר סוג</option>
            <option
              v-for="(type, index) in filters"
              :key="index"
              :value="type.name"
              class="rose-red-text"
            >
              {{ type.name }}
            </option>
          </select>
        </div>

    <div v-for="(menu, index) in selectedMenus" :key="index" class="additional-fields">
      <div class="menu-container">
        <div class="remove-button-wrapper">

        <button class="remove-button"
          @click="
            () => {
              selectedMenus.splice(index, 1)
            }
          "
        >
          &#215;
        </button>
        </div>
        <div class="additional-info">{{ menu.type }}</div>
        <div class="input-field">
          <label for="quantity">כמות</label>
          <input
            id="quantity"
            type="number"
            v-model="menu.quantity"
            placeholder="כמות"
            class="strawberry-pink-bg"
          />
        </div>
        <div class="input-field">
          <label for="price">מחיר ליחידה</label>
          <input
            id="price"
            type="number"
            v-model="menu.price"
            placeholder="מחיר ליחידה"
            class="strawberry-pink-bg"
          />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>


</style>
