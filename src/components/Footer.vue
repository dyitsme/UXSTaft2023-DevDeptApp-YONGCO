<script setup>
import boxicons from 'boxicons'
</script>

<template>
  <footer class="footer">
    <div class="icons">
      <a href="#"><box-icon name='facebook-square' type='logo' color="white" size="md"></box-icon></a>
      <a href="#"><box-icon name='instagram' type='logo' color="white" size="md"></box-icon></a>
      <a href="#"><box-icon name='linkedin-square' type='logo' color="white" size="md"></box-icon></a>
      <a href="#"><box-icon name='github' type='logo' color="white" size="md"></box-icon></a>
    </div>
    <div class="love">
      Made with ♥ by Denzel Yongco
    </div>
  </footer>
</template>

<style scoped>
@import '../assets/main.css';
 .footer {
  display: flex;
  flex-direction: column;
  background-color: var(--dark-grey);
  align-items: center;
  justify-content: center;
  bottom: 0;
 }
 .love {
  color: var(--white);
  font-size: 1.25rem;
 }


</style>