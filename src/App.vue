<template>
  <Start v-if="!start" @start-convert="start = !start"/>
  <div class="cont container-fluid d-flex justify-content-center" v-if="start">
    <Main :current = "currencies" />
  </div>
</template>

<script setup>
import { ref } from "vue"
import Main from "./components/main.vue";
import Start from "./components/hello.vue"

const start = ref(false)

const dateForRequest = ref()
const getDate = ()=>{
  let date = new Date();
  const year = date.getFullYear()
  const month = date.getMonth()+1
  const day = date.getDate()
  dateForRequest.value = `${year}-${month}-${day}`
}
getDate()

const currencies = ref()
const getCurrenc = async ()=>{
  const currenc = await fetch(`https://cbu.uz/ru/arkhiv-kursov-valyut/json/all/${dateForRequest.value}/`)
  const data = await currenc.json()
  currencies.value = data
}
getCurrenc()

</script>

<style scoped>

</style>
