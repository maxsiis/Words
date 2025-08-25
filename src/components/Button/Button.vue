<script setup></script>

<template>
  <button class="button"><slot></slot></button>
</template>

<style scoped>
.button {
  width: 335px;
  height: 68px;
  border: none;
  border-radius: 100px;
  padding: 16px 10px;
  background: var(--button-bg);
  font-family: var(--font);
  font-weight: 400;
  font-size: 24px;
  color: var(--text-primary);
  cursor: pointer;
}
</style>
