<script setup>
import SuccessIcon from '../../icons/SuccessIcon.vue';
import FailedIcon from '../../icons/FailedIcon.vue';

const props = defineProps({
  word: { type: String, required: true },
  translation: { type: String, required: true },
  state: { type: Boolean, required: true },
  status: { type: String, required: true },
  index: { type: Number, required: true },
});

const emit = defineEmits(['flip-card', 'status-change']);

const flip = () => emit('flip-card', { index: props.index });
const changeStatus = (s) =>
  emit('status-change', { index: props.index, status: s });
</script>

<template>
  <div class="card" v-if="status === 'pending'">
    <span class="words">{{ state ? translation : word }}</span>
    <div class="card-border">
      <span class="number">01</span>

      <div v-if="!state" class="text-flip">
        <span class="text" @click="flip">Перевернуть</span>
      </div>

      <div v-else class="button-flip">
        <FailedIcon class="button-upper" @click="changeStatus('failed')" />
        <SuccessIcon class="button-upper" @click="changeStatus('success')" />
      </div>
    </div>
  </div>

  <div class="card" v-else-if="status === 'success'">
    <span class="words">{{ translation }}</span>
    <div class="card-border">
      <SuccessIcon class="text-upper" />
      <span class="number">01</span>
      <span class="text">Завершено</span>
    </div>
  </div>

  <div class="card" v-else>
    <span class="words">{{ translation }}</span>
    <div class="card-border">
      <FailedIcon class="text-upper" />
      <span class="number">01</span>
      <span class="text">Завершено</span>
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
.text-upper {
  position: absolute;
  bottom: 300px;
  left: 50%;
  transform: translateX(-50%);
}
.button-flip {
  position: absolute;
  top: 308px;
  left: 50%;
  transform: translateX(-50%);
  padding: 0 5px;
  display: flex;
  align-items: center;
  gap: 33px;
  background: var(--text-primary);
}
.button-upper {
  width: 20px;
  height: 20px;
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
