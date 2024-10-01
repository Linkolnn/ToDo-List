<script setup>
import { RouterLink, RouterView } from 'vue-router'
import ToDo from '@/components/ToDo.vue'
</script>

<template>
  <ToDo></ToDo>
</template>

<style scoped>
#app {
  display: flex;
  justify-content: center;
  width: 100vw;
  min-height: 100vh;
  padding: 5rem;
}
</style>

