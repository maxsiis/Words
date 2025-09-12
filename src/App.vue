<script setup>
import { ref, computed } from 'vue';
import Button from './components/Button/Button.vue';
import Score from './components/Score/Score.vue';
import Card from './components/Card/Card.vue';

const score = ref(100);
const cards = ref([]);
const error = ref(null);

const gameStarted = ref(false);
const gameCompleted = ref(false);

async function showGame() {
  await loadWords();
  gameStarted.value = true;
  gameCompleted.value = false;
}

async function loadWords() {
  try {
    const res = await fetch('http://localhost:8080/api/random-words');
    if (!res.ok) {
      error.value = await res.text();
      cards.value = [];
      return;
    }

    const payload = await res.json();
    const list = Array.isArray(payload) ? payload : payload?.data ?? [];

    cards.value = list.map((it, i) => ({
      id: i,
      word: it.word,
      translation: it.translation,
      state: false,
      status: 'pending',
    }));

    error.value = null;
  } catch (e) {
    error.value = String(e);
    cards.value = [];
  }
}

function onFlipCard({ index }) {
  const c = cards.value[index];
  if (c && c.status === 'pending') c.state = true;
}

function onStatusChange({ index, status }) {
  const c = cards.value[index];
  if (c) {
    c.status = status;

    if (status === 'success') {
      score.value += 10;
    } else if (status === 'failed') {
      score.value = Math.max(0, score.value - 4);
    }

    // Проверяем, завершена ли игра после каждого изменения статуса
    if (allCardsCompleted.value) {
      gameCompleted.value = true;
    }
  }
}

function restartGame() {
  score.value = 100;
  cards.value = [];
  gameStarted.value = false;
  gameCompleted.value = false;
}

const allCardsCompleted = computed(() => {
  return (
    cards.value.length > 0 &&
    cards.value.every(
      (card) => card.status === 'success' || card.status === 'failed'
    )
  );
});
</script>

<template>
  <div>
    <Score :score="score" />

    <div class="game-container">
      <!-- Карточки 5x5 -->
      <div v-if="gameStarted && !gameCompleted" class="cards-grid">
        <Card
          v-for="(item, index) in cards"
          :key="item.id"
          :word="item.word"
          :translation="item.translation"
          :state="item.state"
          :status="item.status"
          :index="index"
          @flip-card="onFlipCard"
          @status-change="onStatusChange"
        />
      </div>

      <!-- Кнопка начать заново после завершения игры -->
      <div v-if="gameCompleted" class="buttons-container">
        <Button @click="restartGame">Начать заново</Button>
      </div>

      <!-- Кнопка начать игру в начале -->
      <div v-if="!gameStarted && !gameCompleted" class="buttons-container">
        <Button @click="showGame">Начать игру</Button>
      </div>
    </div>

    <div v-if="error" class="error-message">Ошибка: {{ error }}</div>
  </div>
</template>

<style scoped>
.game-container {
  min-height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px 0;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(5, 1fr);
  gap: 15px;
  max-width: 1400px;
  margin: 0 auto;
}

.buttons-container {
  display: flex;
  flex-direction: column;
  gap: 15px;
  align-items: center;
}

.error-message {
  color: red;
  text-align: center;
  margin: 10px 0;
}

@media (max-width: 1200px) {
  .cards-grid {
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(5, 1fr);
  }
}

@media (max-width: 900px) {
  .cards-grid {
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(5, 1fr);
  }
}

@media (max-width: 600px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(5, 1fr);
  }
}
</style>
