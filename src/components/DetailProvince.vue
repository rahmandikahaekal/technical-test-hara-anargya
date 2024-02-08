<template>
  <transition name="fade">
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="w-[500px] bg-white p-8 rounded shadow-md relative">
        
        <button @click="closeModal" class="bg-red-500 hover:bg-red-700 transition duration-300 text-white rounded p-2 absolute right-8">
          <Icon icon="solar:close-square-linear" class="text-2xl" />
        </button>

        <div class="flex mb-2">
          <span v-if="selectedProvince && cities[selectedProvince.id]">
            <h2 class="text-2xl font-bold mb-2">
              Daftar Kota di {{ selectedProvince.name }} :
            </h2>
            <ul class="list-disc pl-5">
              <li
                class="text-xl"
                v-for="city in cities[selectedProvince.id]"
                :key="city.id"
              >
                {{ setCityName(city) }}
              </li>
            </ul>
          </span>
        </div>

      </div>
    </div>
  </transition>
</template>

// Di dalam objek script
<script>
import city from '../city.js';

export default {
  props: {
    isVisible: {
      type: Boolean,
    },
    selectedProvince: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      cities: city,
    };
  },
  methods: {
    setCityName (data) {
      const city_name = data.name;
      return city_name;
    },
    closeModal() {
      this.$emit('close');
    },
    findCityById(cityId) {
      for (const provinceId in this.cities) {
        if (this.cities.hasOwnProperty(provinceId)) {
          const citiesInProvince = this.cities[provinceId];
          const foundCity = citiesInProvince.find(city => city.id === cityId);
          if (foundCity) {
            return foundCity;
          }
        }
      }
      return null; 
    },
  },
};
</script>


<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
