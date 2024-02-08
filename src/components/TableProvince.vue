<template>
  <div class="w-full rounded-[20px] bg-white border border-gray-300">
    <div class="font-bold border-b-2 text-2xl pt-8 pb-5 px-5 rounded-t-[20px]">
      Province List
    </div>
    <table class="w-full bg-white rounded-b-[20px]">
      <thead class="bg-[#fafbfc] text-zinc-400">
        <tr>
          <th class="font-medium text-center py-4 px-3 border-b">ID</th>
          <th class="font-medium text-left py-4 px-4 border-b">Province</th>
          <th class="font-medium text-left py-4 px-4 border-b">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in data" :key="item.id">
          <td class="text-center py-2 px-3 border-b">
            {{ item.id }}
          </td>
          <td class="font-semibold text-left py-2 px-4 border-b">
            <span class="flex items-center">
              {{ item.name }}
            </span>  
          </td>
          <td class="font-semibold text-left py-2 px-4 border-b">
            <button
              class="shadow-md px-8 py-1 rounded-lg hover:bg-[#E3F2FD]"
              @click="openModal(item)"
            >
              View Detail
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <user-detail-modal
      :isVisible="viewDetailProvince"
      :selected-province="selectedDetailProvince"
      @close="closeModal"
    />
  </div>
</template>

<script>
import UserDetailModal from '../components/DetailProvince.vue';

export default {
  components: {
    UserDetailModal
  },
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  data () {
    return {
      viewDetailProvince: false,
      selectedDetailProvince: {}
    }
  },
  mounted () {
    // buat mempermudah user ketika mengklik button detail user untuk menutup tinggal klik esc pada keyboard
    window.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleKeyDown);
  },
  methods: {
    handleKeyDown(event) {
      if (event.key === 'Escape') {
        this.closeModal();
      }
    },
    setNama (data) {
      const first_name = data.first_name
      const last_name = data.last_name
      return first_name + ' ' + last_name
    },
    openModal (userData) {
      console.log('open')
      console.log('userdata', userData)
      this.selectedDetailProvince = userData;
      this.viewDetailProvince = true;
    },
    closeModal () {
      this.selectedDetailProvince = {};
      this.viewDetailProvince = false;
    },
  }
};
</script>
