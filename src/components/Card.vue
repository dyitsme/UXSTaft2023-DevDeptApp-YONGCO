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
  <div class="card-container">
    <div class="card">
      <div class="link-group">
        <p class="long">{{ long }}</p>
        <p class="short">{{ short }}</p>
      </div>
      <div class="empty-group"></div>
    <div class="btn-group">
        <button class="copy-btn" @click="copyToClipBoard"><box-icon name='copy' size="md"></box-icon></button>
        <button class="remove-btn" @click="removeCard"><box-icon name='x' size="md" color="lightgrey"></box-icon></button>
    </div>
    </div>
  </div>
</template>

<style scoped>
@import '../assets/main.css';
.card-container {
  display: flex;
  justify-content: center;
  width: 100vw;
}
.card {
  display: flex;
  font-size: 1.5rem;
  background-color: var(--light-grey);
  justify-content: space-between;
  min-width: 1249px;
  border-radius: 10px;
  margin-top: 20px;
  margin-bottom: 20px;
  padding-left: 20px;
  padding-right: 20px;
}
.link-group {
  display: flex;
  justify-content: space-between;
  flex: 2;
}
.long {
  color: var(--black);
}
.short {
  color: var(--primary-green);
}
.empty-group {
  flex: 1;
}
.btn-group {
  display: flex;
  flex: 1;
}
.copy-btn {
  border: none;
  background-color: var(--light-grey);
  cursor: pointer
}
.remove-btn {
  border: none;
  background-color: var(--light-grey);
  cursor: pointer;
}
</style>