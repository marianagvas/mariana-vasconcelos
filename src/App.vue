<script setup>
import { ref, computed } from 'vue'
import MainPage from './components/MainPage.vue'
import DynamicPage from './components/DynamicPage.vue'
import NotFound from './components/NotFound.vue'
import { data } from './data.js'


const routes = {
  '/': MainPage,
  '/about': NotFound
}

const currentPath = ref(window.location.pathname)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.pathname
})

const currentView = computed(() => {
  if (data.hasOwnProperty(currentPath.value.replace("/", ""))) {
    return DynamicPage
  }
  return routes[currentPath.value || '/'] || NotFound
})
</script>

<template>
  <v-app>
    <AppNavBar />

    <v-main>
      <component :is="currentView" />
    </v-main>

    <AppFooter />
  </v-app>
</template>
