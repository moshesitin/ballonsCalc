    <script setup>
import { ref, reactive, defineEmits } from 'vue'
const selectedType = ref(null)
const quantity = ref(0)
const price = ref(0)
const selectedMenus = reactive([])

const emit = defineEmits(['update-menu'])

const filters = reactive([
  { name: 'עבודה בסיסית' },
  { name: 'עבודה אמנותית' },
  { name: 'עבודה מורכבת' }
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
  <div class="stage3">
    <h2>שלב 3 זמן עבודה</h2>
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

    <div v-for="(menu, index) in selectedMenus" :key="index" class="additional-fields">
      <div class="menu-container">
        <button
          @click="
            () => {
              selectedMenus.splice(index, 1)
            }
          "
        >
          הסר
        </button>
        <div class="additional-info"> {{ menu.type }}</div>
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
</template>


<style scoped>
.strawberry-pink-bg {
  background-color: #ffb6c1;
}

.rose-red-text {
  color: #ff8888;
}
select.custom-select {
  background-color: #ffb6c1;
  border: 2px solid #ff8888;
  color: #000;
  padding: 8px;
  border-radius: 5px;
}

select.custom-select option {
  background-color: #ffb6c1;
  color: #000;
}
input.custom-input {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
input.custom-input {
  background: linear-gradient(to bottom, #ffb6c1, #ff8888);
  border: 2px solid #ff8888;
  color: #000;
  padding: 5px;
  border-radius: 5px;
}
</style>
