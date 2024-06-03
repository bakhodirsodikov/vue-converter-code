<template>
  <div class="main__cont d-flex w-100" 
  :class="{ 'flex-column': convertToUzs === true, 'flex-column-reverse': convertToUzs === false}">
    <div class="d-flex justify-content-between">
      <div class="main__currency d-flex">
        <div class="main__flag">flag</div>
        <div class="dropdown dropdown1">
          <button class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false" >
            {{ drop1Text }}
          </button>
          <ul class="dropdown-menu" >
            <li >
              <a v-for="(cost, idx) in current" :key="idx" class="dropdown-item"  
                href="#" 
                @click="convertTo(idx)">{{cost.Ccy}}</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="main__amount d-flex justify-content-end align-items-center">
        <input class="w-100 main__amount-input rounded" type="number"
        :class="{'pointer-event-none': convertToUzs === false}"
        :v-model="numFrom">
      </div>
    </div>

    <div class="main__arrow d-flex align-items-center">
      <div class="main__arrow-line"></div>
      <button class="main__arrow-arrows d-flex flex-column mx-2 rounded-circle"
      @click="convertToUzs = !convertToUzs">
        <span class="bi bi-chevron-up"></span>
        <span class="bi bi-chevron-down"></span>
      </button>  
      <div class="main__arrow-line"></div>
    </div>

    <div class="d-flex justify-content-between">
      <div class="main__currency d-flex">
        <div class="main__flag">flag</div>
        <div class="dropdown dropdown1">
          <button class="btn btn-secondary " type="button" >
            UZS
          </button>
        </div>
      </div>
      <div class="main__amount d-flex justify-content-end align-items-center">
        <input class="w-100 main__amount-input rounded" type="number"
        :class="{'pointer-event-none': convertToUzs === true}">
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue"

const props = defineProps(['current'])
const drop1Text = ref('Выберите валюту')
const convertToUzs = ref(true)
const numFrom = ref()

const cost2 = ref()
const convertTo = (id)=>{
  cost2.value = props.current[id].Rate
  drop1Text.value = props.current[id].Ccy
  console.log(numFrom);
}



const convertingTo = (num)=>{

}
</script>

<style>
</style>