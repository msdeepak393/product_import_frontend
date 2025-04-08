<script setup>
import { useRoute } from 'vue-router'
import Header from './components/Header.vue'

const route = useRoute()
</script>

<template>
  <div class="container">
  <Header v-if="route.path !== '/login' && route.path !== '/register'" />
    <router-view />
  </div>
</template>

<style scoped>
</style>
