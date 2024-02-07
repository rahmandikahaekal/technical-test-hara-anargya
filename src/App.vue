<template>
  <div class="flex h-screen" id="app">
    <Sidebar />
    <div class="flex flex-col flex-1">
      <Navigation />
      <div class="bg-[#f7f8fa] flex-1 overflow-hidden">
        <RouterView />
      </div>
    </div>
  </div>
</template>

<script>
import { RouterView } from 'vue-router';
import Sidebar from './components/Sidebar.vue';
import Navigation from './components/Navigation.vue';

export default {
  components: {
    Sidebar,
    Navigation
  }
};
</script>

<style scoped>
/* Gaya CSS sesuai kebutuhan */
</style>
