<script setup>
import { ref } from 'vue'

const imgUrl = ref('https://i.pinimg.com/564x/a0/af/fa/a0affa452658c0766686f75dcbfb745f.jpg')
const imageRef = ref(null)

const onFileChange = (e) => {
  const file = e.target.files[0]
  imgUrl.value = URL.createObjectURL(file)
}

const selectedPercent = ref(10)
</script>
    
<template>
  <div class="wrapper1">
    <div class="img">
      <img :src="imgUrl" />
    </div>
    <h2>שלב 1 פרטים</h2>
    <form action="" method="get">
      <input type="text" name="" id="" placeholder="שם העיצוב" />
      <input type="text" name="" id="" placeholder="כמות" />
      <input type="file" accept="image/*" @change="onFileChange"/>
    </form>
    <div class="percent-slider">
      <input type="range" id="percentSlider" min="0" max="100" step="1" v-model="selectedPercent" />
      <div id="selectedPercent">{{ selectedPercent }}%</div>
    </div>
  </div>
</template>

<style scoped>
.wrapper1 {
  height: 500px;
  width: 100vw;
  display: flex;
  flex-direction: row;
  gap: 5px;
}

.img {
  height: 100%;
  width: 50%;
  position: relative; 
}

.img img {
  position: absolute; 
  top: 0;
  left: 0;
  width: 60%;
  height: 60%; 
  object-fit: contain; 
  transition: transform .2s;
}

.img img:hover {
  transform: scale(1.5);
  z-index: 1; 
}

.info {
  height: 50%;
  width: 50%;
}
form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.percent-slider {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

input[type='range'] {
  width: 50%;
}

#selectedPercent {
  top: -30px;
  left: 0;
}
</style>