<script setup>
import Button from "./components/Button.vue"
const date = new Date().toLocaleDateString('ru-RU');
</script>

<template>
  <header>Текущая дата: {{ date }}.</header>
  <main>
    <Button>Начать игру</Button>
  </main>
</template>

<style scoped>
</style>
