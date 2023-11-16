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
    <div class="btn-group">
        <button class="copy-btn" @click="copyToClipBoard"><box-icon name='copy' size="md"></box-icon></button>
        <button class="remove-btn" @click="removeCard"><box-icon name='x' size="md" color="grey"></box-icon></button>
    </div>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  display: flex;
  justify-content: center;
  width: 100vw;
  flex: 1;
}
.card {
  display: flex;
  font-size: 1.5rem;
  background-color: var(--light-grey);
  justify-content: space-around;
  width: 1449px;
  border-radius: 10px;
  margin-top: 30px;
  margin-bottom: 30px;
  padding-left: 20px;
  padding-right: 20px;
}
.link-group {
  display: flex;
  justify-content: space-between;
  flex: 4;
}
.long {
  color: var(--black);
}
.short {
  color: var(--primary-green);
}
.btn-group {
  display: flex;
  flex: 1;
  justify-content: flex-end;
}
.copy-btn {
  border: none;
  background-color: var(--light-grey);
  cursor: pointer
}
.copy-btn:hover {
  background-color: var(--grey);
  transition: 0.5s;
}
.remove-btn {
  border: none;
  background-color: var(--light-grey);
  cursor: pointer;
}
.remove-btn:hover {
  background-color: var(--grey);
  transition: 0.5s;
}

.remove-btn:active {
  background-color: var(--dark-grey);
  transition: 0.5s;
}
</style>