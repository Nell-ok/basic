<script setup>
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"

const like = {
  number: 100,
};
</script>

<template>
  <header class="header">
    <div class="header__container">
      <p>Запомни слово</p>
      <Score v-bind="like" />
    </div>
  </header>
  <main>
    <Button>Начать игру</Button>
  </main>
</template>

<style scoped>
.header {
  margin: 0 62px;
}
.header__container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 37px 0;
}
.header p {
  margin: 0;
  padding: 0;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-basic-dark);
}
</style>
