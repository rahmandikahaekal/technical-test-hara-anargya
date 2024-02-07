<template>
  <div class="h-screen">
    <!-- Sidebar -->
    <aside class="bg-white text-gray-800 w-64 flex-shrink-0 shadow-md h-full">
      <!-- Sidebar Content -->
      <div class="p-4">
        <!-- Logo -->
        <div class="text-3xl font-inter font-extrabold">
          heylink.
        </div>

        <!-- Sidebar Links -->
        <nav class="mt-4">
          <router-link
            to="/"
            class="text-xl block font-medium py-2 px-4 text-gray-800 hover:bg-gray-200 hover:rounded-[8px] transition duration-300 flex items-center"
            :class="{ 'bg-[#E3F2FD] rounded-[8px]': $route.path === '/' }"
          >
            <Icon icon="solar:graph-down-outline" class="mr-2" />
            Home
          </router-link>
          <router-link
            to="/overview"
            class="text-xl block font-medium py-2 px-4 text-gray-800 hover:bg-gray-200 hover:rounded-[8px] transition duration-300 flex items-center"
            :class="{ 'bg-[#E3F2FD] rounded-[8px]': $route.path === '/overview' }"
          >
            <Icon icon="solar:graph-up-outline" class="mr-2" />
            Overview
          </router-link>
        </nav>
      </div>
      <!-- End Sidebar Content -->
    </aside>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
}
</script>

<style scoped>
/* Add your custom styles here */
</style>
