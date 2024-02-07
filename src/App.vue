<template>
  <div class="flex h-screen overflow-hidden" id="app">
    <div class="overflow-x-hidden">
      <Sidebar />
    </div>
    <div class="flex flex-col flex-1 overflow-hidden">
      <Navigation />
      <div class="bg-[#f7f8fa] flex-1 overflow-y-auto">
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
