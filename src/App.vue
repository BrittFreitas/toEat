<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header>
  <div class="container">
     <h1>toEat</h1>
     <RouterView class="test" />
  </div>
   
    
  </header>

 
</template>

<style scoped>
.container h1 {
  display: flex;
  justify-content: center;
}
</style>
