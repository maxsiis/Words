<script setup>
import ScoreIcon from '../../icons/ScoreIcon.vue';
const { score } = defineProps({
  score: Number,
});
</script>

<template>
  <div class="header">
    <h1>Запомни слово</h1>
    <div class="score">
      <span>{{ score }}</span>
      <ScoreIcon />
    </div>
  </div>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 37px 62px 0 62px;
}
h1 {
  font-family: var(--font);
  font-weight: 700;
  font-size: 16px;
}
.score {
  width: 110px;
  height: 48px;
  background: #cce8ff;
  border-radius: 36px;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
span {
  color: var(--button-bg);
  font-family: var(--font);
  font-weight: 700;
  font-size: 16px;
}
</style>
