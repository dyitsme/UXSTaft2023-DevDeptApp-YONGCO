<script setup>

const { long, short } = defineProps(['long', 'short'])
const emit = defineEmits(['copy', 'delete'])

function copyToClipBoard() {
  emit('copy')
}

function removeCard() {
  emit('remove')
}
</script>
<template>
  <div>
      {{ long }} {{ short }}
      <button class="copy-btn" @click="copyToClipBoard">Copy to Clipboard</button>
      <button class="remove-btn" @click="removeCard">Delete</button>
  </div>
</template>