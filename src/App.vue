<script setup>
import { ref, onMounted } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const like = ref({
  number: 100,
});

const cards = ref([]);

async function getCards() {
  const response = await fetch('http://localhost:8080/api/random-words')
  const data = await response.json()
  
  cards.value = data.map(card => ({
    ...card,
    state: 'close',
    status: 'pending',
    id: `${card.word}-${Math.random()}`
  }))
};

onMounted(getCards);

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
        <Card v-bind="{ ...card, ...contentButton, ...contentNumber }" @flip="onFlip()" />
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
  margin-bottom: 100px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  column-gap: 100px;
  row-gap: 66px;
}
</style>
