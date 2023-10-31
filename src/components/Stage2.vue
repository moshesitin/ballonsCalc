    <script setup>
import { ref, reactive, computed, defineProps, defineEmits } from 'vue'
const selectedCategory = ref(null)
const selectedSubcategory = ref(null)
const selectedType = ref(null)
const selectedTypes = reactive([])
const quantity = ref(0)
const price = ref(0)
const selectedMenus = reactive([])

const emit = defineEmits(['update-menu'])

const filters = reactive([
  {
    category: 'בלונים',
    subCategory: [
      {
        name: 'בלוני לטקס',
        type: [
          `5"`,
          `9"/10"`,
          `11"/12"`,
          `16"`,
          `18"/19"`,
          `24"`,
          `3"/36"`,
          `160`,
          `260`,
          `350`,
          `646`,
          `לינק 6"`,
          `לינק 12"`,
          `לטקס שונות/מיוחדים`
        ]
      },
      {
        name: 'בלוני מיילר',
        type: [
          `4"`,
          `7"-9"`,
          `14"-16"`,
          `18"-20"`,
          `22"-24"`,
          `30"-32"`,
          `34"-36"`,
          `38"-40"`,
          ` '+50"`
        ]
      },
      { name: `אקווה\בובו`, type: [`4"`, `14"`, `18"/20"`, `22"/24"`, `36"`] },
      {
        name: 'באבל',
        type: [`שקוף 20"`, `שקוף 24"`, `דקו באבל "20/"24`, `סינגל באבל "20/"22`, `דאבל באבל`]
      },
      { name: 'אורבז', type: [`מיני`, `רגיל`, `ג'אמבו`] }
    ]
  },
  {
    category: 'הליום',
    subCategory: [
      {
        name: 'בלוני לטקס',
        type: [`9"/10"`, `11"/12"`, `16"`, `18"/19"`, `24"`, `3"/36"`, `לינק 12"`]
      },
      {
        name: 'בלוני מיילר',
        type: [`14"-16"`, `18"-20"`, `22"-24"`, `30"-32"`, `34"-36"`, `38"-40"`, ` '+50"`]
      },
      { name: `אקווה\ובוב`, type: [`14"`, `18"/20"`, `22"/24"`, `30"-32"`, `36"`] },
      {
        name: 'באבל',
        type: [`שקוף 20"`, `שקוף 24"`, `דקו באבל 20/24"`, `סינגל באבל 20"/"22"`, `דאבל באבל`]
      },
      { name: 'אורבז', type: [`רגיל`, `ג'אמבו`] }
    ]
  },
  {
    category: 'ציוד',
    subCategory: [
      { name: 'דבקים', type: [`בלון בונד`, `סטרצ'י`, `גלו גוטס`, `חבקים`, `דבק אחר`] },
      { name: `בדים\םסרטי`, type: [`בד טול`, `סרט סטן`, `סרט מתנה`] },
      {
        name: `סטנדים\תקונסתרוקציו`,
        type: [
          `סטנד שולחן`,
          `סטנד רצפה`,
          `קשתות`,
          `לוח קאפה`,
          `לוח פי וי סי`,
          `לוח פרספקט`,
          `שונות`
        ]
      },
      {
        name: `שונות`,
        type: [
          `אקססוריז`,
          `ספריי צבע`,
          `בלון שיין/היי שיין`,
          `הייפלוט`,
          `חוט דיג`,
          `מוט גמיש`,
          `מדבקות ויניל`,
          `שונות`
        ]
      }
    ]
  },
  // {
  //   category: 'שעות עבודה',
  //   subCategory: [{ name: 'עבודה בסיסית' }, { name: 'עבודה אמנותית' }, { name: 'עבודה מורכבת' }]
  // },
  // {
  //   category: 'עלויות כלליות',
  //   subCategory: [
  //     { name: 'זמן עבודה כללי' },
  //     { name: 'משלוח' },
  //     { name: 'עובדים' },
  //     { name: 'שונות' }
  //   ]
  // }
])
const selectedCategorySubcategories = computed(() => {
  // selectedCategorySubcategories in return contains array with names of subcategorys
  const category = filters.find((item) => item.category === selectedCategory.value)
  return category ? category.subCategory.map((sub) => sub.name) : []
})

const selectedSubcategoryTypes = computed(() => {
  // like selectedCategorySubcategories 👆 just for containig of types
  const category = filters.find((item) => item.category === selectedCategory.value)
  if (category) {
    const subcategory = category.subCategory.find((sub) => sub.name === selectedSubcategory.value)
    return subcategory ? subcategory.type : []
  }
  return []
})

const addNewMenu = () => {
  // create info for menu

  if (selectedCategory && selectedSubcategory) {
    const menu = {
      subcategory: selectedSubcategory.value,
      quantity: quantity.value,
      price: price.value
    }
    if (selectedType.value) {
      menu.type = selectedType.value
      selectedTypes.push(selectedType.value)
      selectedType.value = null
    }
    selectedMenus.push(menu)
    quantity.value = 0
    price.value = 0
  }

  // if (selectedCategory && selectedSubcategory) {
  //   selectedMenus.push({
  //     subcategory: selectedSubcategory,
  //     type: selectedType.value, // Обновите эту строку
  //     quantity: quantity.value, // Обновите эту строку
  //     price: price.value // Обновите эту строку
  //   })
  //   selectedTypes.push(selectedType.value) // Добавьте выбранный тип в массив
  //   selectedType.value = null // Обнулите выбранный тип
  //   quantity.value = 0 // Обнулите количество
  //   price.value = 0 // Обнулите цену
  // }
}
emit('update-menu', selectedMenus)
const addNewMenuSub = () => {
  if (!selectedSubcategoryTypes.value) {
    addNewMenu()
  }
}

selectedType.value = null
</script>
    
<template>
  <div class="stage2">
    <h2>שלב 2 בחר חומרים</h2>
    <select v-model="selectedCategory" class="strawberry-pink-bg">
      <option disabled value="" class="rose-red-text">בחר אחת מהקטגוריות</option>
      <option
        v-for="(category, index) in filters"
        :key="index"
        :value="category.category"
        class="rose-red-text"
      >
        {{ category.category }}
      </option>
    </select>

    <select
      v-model="selectedSubcategory"
      v-if="selectedCategory"
      @change="addNewMenuSub"
      class="strawberry-pink-bg"
    >
      <option disabled value="" class="rose-red-text">בחר תתקטגוריה</option>
      <option
        v-for="(subcategory, index) in selectedCategorySubcategories"
        :key="index"
        :value="subcategory"
        class="rose-red-text"
      >
        {{ subcategory }}
      </option>
    </select>

    <select
      v-model="selectedType"
      v-if="selectedSubcategory"
      @change="addNewMenu"
      class="strawberry-pink-bg"
    >
      <option disabled value="" class="rose-red-text">בחר סוג</option>
      <option
        v-for="(type, index) in selectedSubcategoryTypes"
        :key="index"
        :value="type"
        class="rose-red-text"
      >
        {{ type }}
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
        <div class="additional-info">{{ menu.subcategory }} {{ menu.type }}</div>
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
        <select
          v-model="selectedTypes[index]"
          @change="(event) => (menu.type = event.target.value)"
        >
          <option disabled value="" class="rose-red-text">שנה סוג</option>
          <option
            v-for="(type, index) in selectedSubcategoryTypes"
            :key="index"
            :value="type"
            class="rose-red-text"
          >
            {{ type }}
          </option>
        </select>
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
