<template>
  <transition name="fade">
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="w-[700px] bg-white p-8 rounded shadow-md relative">
        
        <button @click="closeModal" class="bg-red-500 hover:bg-red-700 transition duration-300 text-white rounded p-2 absolute right-8">
          <Icon icon="solar:close-square-linear" class="text-2xl" />
        </button>
        <h2 class="text-2xl font-bold mb-2">
          Daftar Kota di {{ selectedProvince.name }} :
        </h2>

        <div class="flex mt-10 mb-2 overflow-y-auto h-[450px]">
          <ul class="list-disc pl-5">
            <li
              class="text-xl"
              v-for="city in cityBaseOnProvince"
              :key="city.id"
            >
              {{ setCityName(city) }}
            </li>
          </ul>
        </div>

      </div>
    </div>
  </transition>
</template>

// Di dalam objek script
<script>
import city from '../assets/js/city';

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
      cityBaseOnProvince: [],
    };
  },
  watch: {
    isVisible: {
      deep: true,
      handler () {
        console.log('updated')
        this.filterCity()
      }
    }
  },
  computed: {
  },
  mounted () {
  },
  methods: {
    setCityName (data) {
      const city_name = data.name;
      return city_name;
    },
    closeModal() {
      this.$emit('close');
    },
    filterCity() {
      const data = this.cities.filter( (city) => city.provinsi_id === this.selectedProvince.id);
      this.cityBaseOnProvince = data
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
