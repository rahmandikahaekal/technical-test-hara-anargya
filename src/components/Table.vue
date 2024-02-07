<template>
  <div class="w-full rounded-[20px] bg-white border border-gray-300">
    <div class="font-bold border-b-2 text-2xl pt-8 pb-5 px-5 rounded-t-[20px]">
      User List
    </div>
    <table class="w-full bg-white rounded-b-[20px]">
      <thead class="bg-[#fafbfc] text-zinc-400">
        <tr>
          <th class="font-medium text-center py-4 px-2 border-b">ID</th>
          <th class="font-medium text-left py-4 px-4 border-b">User</th>
          <th class="font-medium text-left py-4 px-4 border-b">Date Of Birth</th>
          <th class="font-medium text-left py-4 px-4 border-b">Email</th>
          <th class="font-medium text-left py-4 px-4 border-b">Job</th>
          <th class="font-medium text-left py-4 px-4 border-b">Country</th>
          <th class="font-medium text-left py-4 px-4 border-b">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in data" :key="item.id">
          <td class="text-center py-2 px-2 border-b">
            {{ item.id }}
          </td>
          <td class="font-semibold text-left py-2 px-4 border-b">
            <span class="flex items-center">
              <img :src="item.profile_picture" class="rounded-full w-6 h-6 object-cover"/>
              <span class="ml-2">
                {{ setNama(item) }}
              </span>
            </span>  
          </td>
          <td class="text-slate-500 font-normal text-left py-2 px-4 border-b">
            {{ formatDate(item.date_of_birth) }}
          </td>
          <td class="font-semibold text-left py-2 px-4 border-b">{{ item.email }}</td>
          <td class="text-slate-500 font-normal text-left py-2 px-4 border-b">
            {{ item.job }}
          </td>
          <td class="font-semibold text-left py-2 px-4 border-b">{{ item.country }}</td>
          <td class="font-semibold text-left py-2 px-4 border-b">
            <button class="shadow-md px-8 py-1 rounded-lg mr-2">
              Select
            </button>
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
      :isVisible="viewDetailuser"
      :selected-user="selectedDetailUser"
      @close="closeModal"
    />
  </div>
</template>

<script>
import UserDetailModal from '../components/DetailUser.vue';

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
      viewDetailuser: false,
      selectedDetailUser: {}
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
    formatDate (dateString) {
      const options = { year: 'numeric', month: '2-digit', day: '2-digit' };
      const formattedDate = new Date(dateString).toLocaleDateString(undefined, options);
      return formattedDate;
    },
    
    openModal (userData) {
      console.log('open')
      console.log('userdata', userData)
      this.selectedDetailUser = userData;
      this.viewDetailuser = true;
    },
    closeModal () {
      this.selectedDetailUser = {};
      this.viewDetailuser = false;
    },
  }
};
</script>
