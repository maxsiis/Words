<script setup>
import Button from './components/Button/Button.vue';
import Score from './components/Score/Score.vue';
import Card from './components/Card/Card.vue';
import { computed, ref } from 'vue';

const score = ref(100);
const data = ref([]);
const error = ref();

const displayGame = ref(false);
const displayButton = ref(true);

async function showGame() {
  await getWord();
  displayGame.value = true;
  displayButton.value = false;
  console.log('карты показаны');
}

function FlipCard(card) {
  console.log(card);
}

const dataModified = computed(() => {
  if (!data.value) return [];
  return [
    {
      word: data.value.word,
      translation: data.value.translation,
      state: false,
      status: 'pending',
    },
    {
      word: data.value.word,
      translation: data.value.translation,
      state: true,
      status: 'success',
    },
    {
      word: data.value.word,
      translation: data.value.translation,
      state: true,
      status: 'failed',
    },
  ];
});
async function getWord() {
  const res = await fetch('http://localhost:8080/api/random-words');
  if (res.status != 200) {
    data.value = null;
    error.value = await res.json();
  }
  error.value = null;
  data.value = await res.json();
}
</script>

<template>
  <div>
    <div class="card-items" v-if="displayGame">
      <Card
        v-for="item in dataModified"
        :key="item.word"
        :word="item.word"
        :translation="item.translation"
        :state="item.state"
        :status="item.status"
      />
    </div>
    <div>
      <Score :score="score" />
      <div class="app-container">
        <Button v-if="displayButton" @click="showGame">Начать игру</Button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
