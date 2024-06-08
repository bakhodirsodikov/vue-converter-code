<template>
  <div class="welcome cont container-fluid d-flex flex-column justify-content-center align-items-center ">
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
    <button class="welcome-btn btn bi bi-play-btn mt-4" @click="$emit('startConvert')"></button>
  </div>
</template>

<script setup>

const emits = defineEmits(['startConvert',])
</script>

<style scoped>

</style>