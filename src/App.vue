<template>
  <div v-if="!start" class="welcome cont container-fluid d-flex flex-column justify-content-center align-items-center ">
    <div class="title-cont">
      <span class="title-box d-flex flex-column text-center">
        <h2 class="title ">Привет 👋🏻</h2>
        <h2 class="title ">Добро пожаловать</h2>
        <h2 class="title ">В</h2>
        <h2 class="title ">Самый</h2>
        <h2 class="title ">Лучший</h2>
        <h2 class="title ">Конвертер 🔄💰</h2>
      </span>
    </div>
    <button class="welcome-btn btn bi bi-play-btn mt-4" @click="start = !start"></button>
  </div>
  <div class="cont container-fluid d-flex justify-content-center" v-if="start">
    <Main :current = "currencies" />
  </div>
</template>

<script setup>
import { ref } from "vue"
import Main from "./components/main.vue";

const start = ref(true)

const dateForRequest = ref()
const getDate = ()=>{
  let date = new Date();
  const year = date.getFullYear()
  const month = date.getMonth()+1
  const day = date.getDate()
  dateForRequest.value = `${year}-${month}-${day}`
}
getDate()

const getCurrenc = async ()=>{
  const currenc = await fetch(`https://cbu.uz/ru/arkhiv-kursov-valyut/json/all/${dateForRequest.value}/`)
  const data = await currenc.json()
  currencies.value = data
  console.log(data);
}
getCurrenc()

const currencies = ref()

  

</script>

<style scoped>

</style>
