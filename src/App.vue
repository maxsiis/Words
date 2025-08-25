<script setup>
import Button from './components/Button/Button.vue';
import Score from './components/Score/Score.vue';
import Card from './components/Card/Card.vue';
import { computed, ref } from 'vue';

const score = ref(100);
const data = ref({
  word: 'Carom',
  translation: 'Свинец',
  state: false,
  status: 'success' | 'fail' | 'pending',
});

function FlipCard(card) {
  console.log(card);
}
</script>

<template>
  <Card v-bind="data" @flipCard="FlipCard" />
  <div>
    <Score :score="score" />
    <div class="app-container">
      <Button>Начать игру</Button>
    </div>
  </div>
</template>

<style scoped></style>
