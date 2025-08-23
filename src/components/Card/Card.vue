<script setup>
const emit = defineEmits(['flipCard', 'statusChange']);

const Flip = () => {
  emit('flipCard', 'Карта перевернута');
};

const changeStaus = () => {
  emit('statusChange', 'Статус изменен');
};
</script>

<template>
  <div class="card">
    <span class="words">Pollinatio</span>
    <div class="card-border">
      <span class="number">01</span>
      <span class="text" @click="Flip">Перевернуть</span>
    </div>
  </div>
</template>

<style scoped>
.card {
  background: var(--text-primary);
  width: 250px;
  height: 376px;
  border-radius: 16px;
  margin: 0 auto;
  position: relative;
  padding: 29px 19px;
  box-sizing: border-box;
}

.card:hover {
  box-shadow: 10px 10px 10px 0px rgba(0, 0, 0, 0.05);
}
.card-border {
  border: 1px solid #cce8ff;
  border-radius: 12px;
  width: 100%;
  height: 100%;
  position: relative;
}

.number {
  position: absolute;
  top: -8px; /* Половина высоты текста */
  left: 18%;
  transform: translateX(-50%);
  background: var(--text-primary);
  padding: 0 5px;
  font-family: var(--font);
  font-size: 14px;
  font-weight: 400;
  color: #222222;
}

.text {
  position: absolute;
  top: 311px; /* Половина высоты текста */
  left: 50%;
  transform: translateX(-50%);
  padding: 0 5px;
  background: var(--text-primary);
  font-family: var(--font);
  font-size: 12px;
  font-weight: 700;
  color: #222222;
  text-transform: uppercase;
  letter-spacing: 1px;
}
.words {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: var(--font);
  font-size: 18px;
  font-weight: 400;
  color: #000000;
  z-index: 3;
  white-space: nowrap;
}
</style>
