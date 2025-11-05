<script setup>
import { ref, onMounted } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const score = ref(100);

const cards = ref([]);

async function getCards() {
  const response = await fetch('http://localhost:8080/api/random-words')
  const data = await response.json()
  
  cards.value = data.map((card, index) => ({
    ...card,
    number: (index + 1).toString().padStart(2, 0),
    state: 'close',
    status: 'pending',
    id: `${card.word}-${Math.random()}`
  }))

  score.value = 100
};

onMounted(getCards);

const contentButton = {
  buttonTextClose: 'перевернуть',
  buttonTextOpen: 'завершено',
};

function onFlip(cardId) {
  const card = cards.value.find((c) => c.id === cardId);
  if (card) {
    card.state = 'open';
  }
}

function onChanged({id, status}) {
  const card = cards.value.find((c) => c.id === id);
  if (card && card.status !== status) { // если меняется статус

    if (card.status === 'success' && status === 'fail') {
      score.value -= 14; 
    }
    else if (card.status === 'fail' && status === 'success') {
      score.value += 14;
    }
    // стандартные действия, если переход из "pending"
    else if (card.status === 'pending' && status === 'success') {
      score.value += 10;
    }
    else if (card.status === 'pending' && status === 'fail') {
      score.value -= 4;
    }
    card.status = status;
  }
}

function onReset(cardId) {
  const card = cards.value.find((c) => c.id === cardId);
  if (card) {
    card.state = 'close';
    card.status = 'pending';
  }
}
</script>

<template>
  <header class="center header">
    <div class="header__container">
      <p>Запомни слово</p>
      <Score :number="score" />
    </div>
  </header>
  <main class="center">
    <div class="wrapper">
      <div class="card-list">
        <div v-for="card in cards" :key="card.id">
          <Card
          v-bind="card"
          :button-text-close="contentButton.buttonTextClose"
          :button-text-open="contentButton.buttonTextOpen"
          @flip="onFlip"
          @status-changed="onChanged"
          @reset="onReset" />
        </div>
      </div>
      <Button @click="getCards()">Начать заново</Button>
    </div>
  </main>
</template>

<style scoped>
.center {
  margin: 0 62px;
}
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 65px;
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
