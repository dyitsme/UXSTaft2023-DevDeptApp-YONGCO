<script setup>
import boxicons from 'boxicons'
const { long, short } = defineProps(['long', 'short', 'index'])
const emit = defineEmits(['copy', 'delete'])

function copyToClipBoard() {
  emit('copy')
}

function removeCard() {
  emit('remove')
}
</script>
<template>
  <div class="card">
      <p>{{ long }}</p>
      <p>{{ short }}</p>
      <button class="copy-btn" @click="copyToClipBoard"><box-icon name='copy'></box-icon></button>
      <button class="remove-btn" @click="removeCard"><box-icon name='x' ></box-icon></button>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  font-size: 1.5rem;
  background-color: var(--light-grey);
}
</style>