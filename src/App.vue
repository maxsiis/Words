<script setup>
import Button from './components/Button/Button.vue';
import Score from './components/Score/Score.vue';
import Card from './components/Card/Card.vue';
import { computed, ref } from 'vue';

const score = ref(100);
const data = ref([
  {
    word: 'Carom',
    translation: 'Свинец',
    state: false,
    status: 'pending',
  },
  {
    word: 'Car',
    translation: 'Автомобиль',
    state: true,
    status: 'pending',
  },
  {
    word: 'Duck',
    translation: 'Утка',
    state: true,
    status: 'success',
  },
  {
    word: 'Foreman',
    translation: 'Бригадир',
    state: true,
    status: 'failed',
  },
]);

function FlipCard(card) {
  console.log(card);
}
</script>

<template>
  <div>
    <Card
      v-for="(card, index) in data"
      :key="index"
      v-bind="card"
      @flipCard="FlipCard"
    />
    <div>
      <Score :score="score" />
      <div class="app-container">
        <Button>Начать игру</Button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
