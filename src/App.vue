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
    id: 1,
    states: [
      { state: "close", status: "pending", word: 'unadmitted' },
      { state: "open", status: "pending", translation: 'непризнанный' },
      { state: "open", status: "success", translation: 'непризнанный' },
      { state: "open", status: "fail", translation: 'непризнанный' },
    ]
  },
  {
    id: 2,
    states: [
      { state: "close", status: "pending", word: 'armour-piercer' },
      { state: "open", status: "pending", translation: 'бронебойщик' },
      { state: "open", status: "success", translation: 'бронебойщик' },
      { state: "open", status: "fail", translation: 'бронебойщик' },
    ]
  }
]);

const contentButton = {
  buttonTextClose: 'перевернуть',
  buttonTextOpen: 'завершено',
};

const contentNumber = {
  number: '01',
};

function onFlip() {
  alert('Перевернулась');
}
</script>

<template>
  <header class="center header">
    <div class="header__container">
      <p>Запомни слово</p>
      <Score v-bind="like" />
    </div>
  </header>
  <main class="center">
    <div class="card-list">
      <div v-for="card in cards" :key="card.id">
        <div v-for="(state, i) in card.states" :key="i">
          <Card v-bind="{ ...state, ...contentButton, ...contentNumber }" @flip="onFlip()" />
        </div>
      </div>
    </div>
    <Button>Начать игру</Button>
  </main>
</template>

<style scoped>
.center {
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
  display: flex;
  justify-content: space-between;
}
</style>
