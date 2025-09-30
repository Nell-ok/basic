<script setup>
import { ref } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const like = ref({
  number: 100,
});

const cards = ref([
  {
    word: 'unadmitted',
    translation: 'непризнанный',
    state: 'close',
    statuse: 'pending',
  },

  {
    word: 'armour-piercer',
    translation: 'непризнанный',
    state: 'close',
    statuse: 'pending',
  },

  {
    word: 'stamen',
    translation: 'бронебойщик',
    state: 'close',
    statuse: 'pending',
  }
]);

const contentButton = {
  buttonText: 'перевернуть',
};

const contentNumber = {
  number: '01',
};

function onFlip() {
  alert('Перевернулась');
}
</script>

<template>
  <header class="header">
    <div class="header__container">
      <p>Запомни слово</p>
      <Score v-bind="like" />
    </div>
  </header>
  <main>
    <ul class="card-list">
      <Card v-bind="{ ...cards[0], ...contentButton, ...contentNumber }" @flip="onFlip()" />
    </ul>
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
.card-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
</style>
