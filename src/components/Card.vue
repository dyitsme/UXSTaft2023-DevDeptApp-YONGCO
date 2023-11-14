<script setup>

const { long, short } = defineProps(['long', 'short'])
const emit = defineEmits()

function copyToClipBoard() {
  emit('copy')
}

function removeCard() {
  emit('delete')
}
</script>
<template>
  <div>
      {{ long }} {{ short }}
      <button class="copy-btn" @click="copyToClipBoard">Copy to Clipboard</button>
      <button class="remove-btn" @click="removeCard">Delete</button>
  </div>
</template>