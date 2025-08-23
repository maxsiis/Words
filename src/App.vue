<script setup>
import Button from './components/Button/Button.vue';
import Score from './components/Score/Score.vue';
import Card from './components/Card/Card.vue';

const score = 100;
function FlipCard(card) {
  console.log(card);
}
</script>

<template>
  <!-- <Card @flipCard="FlipCard" /> -->
  <div>
    <Score :score="score" />
    <div class="app-container">
      <Button>Начать игру</Button>
    </div>
  </div>
</template>

<style scoped></style>
