<script setup>
import boxicons from 'boxicons'
</script>

<template>
  <footer class="footer">
    <div class="icons">
      <a href="https://www.instagram.com/denzelyongco/"><box-icon name='instagram' type='logo' color="white" size="md"></box-icon></a>
      <a href="https://www.linkedin.com/in/denzel-yongco/"><box-icon name='linkedin-square' type='logo' color="white" size="md"></box-icon></a>
      <a href="https://github.com/dyitsme"><box-icon name='github' type='logo' color="white" size="md"></box-icon></a>
    </div>
    <div class="love">
      Made with ♥ by Denzel Yongco
    </div>
  </footer>
</template>

<style scoped>
 .footer {
  display: flex;
  flex-direction: column;
  background-color: var(--dark-grey);
  align-items: center;
  justify-content: space-around;  
  margin-top: auto;
  min-height: 10vh;
  /* width: 100vw; */
 }
 .love {
  color: var(--white);
  font-size: 1.25rem;
 }


</style>