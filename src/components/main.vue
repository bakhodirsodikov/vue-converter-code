<template>
  <div class="main__cont d-flex w-100" 
  :class="{ 'flex-column': convertTo2 === true, 'flex-column-reverse': convertTo2 === false}">
    <div class="d-flex justify-content-between">
      <div class="main__currency d-flex">
        <div class="dropdown dropdown1">
          <button class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false" >
            {{ drop1Text }}
          </button>
          <ul class="dropdown-menu" >
            <li >
              <a v-for="(cost, idx) in current" :key="idx" class="dropdown-item"  
                href="#" 
                @click="convert1(idx);">{{cost.Ccy}}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="main__amount d-flex justify-content-end align-items-center">
        <input class="w-100 main__amount-input rounded" type="number"
        :class="{'pointer-event-none': convertTo2 === false}"
        v-model="num1">
      </div>
    </div>

    <div class="main__arrow d-flex align-items-center">
      <div class="main__arrow-line"></div>
      <button class="main__arrow-arrows d-flex flex-column mx-2 rounded-circle"
        @click="arrowChange">
        <span class="bi bi-chevron-up"></span>
        <span class="bi bi-chevron-down"></span>
      </button>  
      <div class="main__arrow-line"></div>
    </div>

    <div class="d-flex justify-content-between">
      <div class="main__currency d-flex">
        <div class="dropdown dropdown1">
          <button class="btn btn-secondary pointer-event-none" type="button" >
            UZS
          </button>
        </div>
      </div>
      <div class="main__amount d-flex justify-content-end align-items-center">
        <input class="w-100 main__amount-input rounded" type="number"
        :class="{'pointer-event-none': convertTo2 === true}"
        v-model="num2">
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, watchEffect } from "vue"

const props = defineProps(['current'])
const drop1Text = ref('Выберите валюту')
const convertTo2 = ref(true)
const num1 = ref()
const num2 = ref()

const currency = ref()

const cost = ref()

const convert1 = (id)=>{
  if (convertTo2.value) {
    num1.value = 1
    currency.value = props.current[id]
    drop1Text.value = props.current[id].Ccy
    cost.value = props.current[id].Rate
    num2.value = currency.value.Rate
  }
  else{
    num2.value = 1
    currency.value = props.current[id]
    drop1Text.value = props.current[id].Ccy
    cost.value = props.current[id].Rate
    num1.value = currency.value.Rate
  }
  
}

const arrowChange = ()=>{
  if (convertTo2.value && currency.value) {
    convertTo2.value = !convertTo2.value
    num2.value = 1
  }
  else if (!convertTo2.value && currency.value){
    convertTo2.value = !convertTo2.value
    num1.value = 1
  }
  else{
    convertTo2.value = !convertTo2.value
  }
  
}


watchEffect(()=>{
  if(drop1Text.value !== 'Выберите валюту' && convertTo2.value){
    num2.value = (currency.value.Rate * num1.value).toFixed(2)
  }
})

watch(num2, ()=>{
  if(!convertTo2.value && drop1Text.value !== 'Выберите валюту'){
    num1.value = (num2.value/currency.value.Rate).toFixed(2)
  }
})
  


</script>

<style>
</style>