<template>
  <transition name="fade">
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="w-[500px] bg-white p-8 rounded shadow-md relative">
        <button @click="closeModal" class="bg-red-500 hover:bg-red-700 transition duration-300 text-white rounded p-2 absolute right-5 top-5">
          <Icon icon="solar:close-square-linear" class="text-2xl" />
        </button>

        <div class="flex mb-2">
          <img :src="selectedUser.profile_picture" class="w-20 h-20 object-cover rounded-full mr-4" />
          <div>
            <h2 class="text-2xl font-bold mb-4">
              {{ setNama(selectedUser) }}
            </h2>
            <p>{{ selectedUser.email }}</p>
            <p>{{ selectedUser.phone }}</p>
          </div>  
        </div>

        <div class="flex flex-row">
          <div class="basis-2/5 flex flex-col pr-2">
            <div class="flex justify-between pb-2">
              <span>
                Date Of Birth
              </span>
              <span>
                :
              </span>
            </div>
            <div class="flex justify-between pb-2">
              <span>
                Gender
              </span>
              <span>
                :
              </span>
            </div>
            <div class="flex justify-between pb-2">
              <span>
                Job
              </span>
              <span>
                :
              </span>
            </div>
            <div class="flex justify-between pb-2">
              <span>
                Address
              </span>
              <span>
                :
              </span>
            </div>
            
            <div class="flex justify-between pb-2">
              <span>
                City
              </span>
              <span>
                :
              </span>
            </div>
            <div class="flex justify-between pb-2">
              <span>
                State
              </span>
              <span>
                :
              </span>
            </div>
            <div class="flex justify-between pb-2">
              <span>
                Country
              </span>
              <span>
                :
              </span>
            </div>
          </div>
          <div class="basis-3/5">
            <div class="pb-2">
              {{ formatDate(selectedUser.date_of_birth) }}
            </div>
            <div class="pb-2">
              {{ selectedUser.gender }}
            </div>
            <div class="pb-2">
              {{ selectedUser.job }}
            </div>
            <div class="pb-2">
              {{ selectedUser.street }}
            </div>
            <div class="pb-2">
              {{ selectedUser.city }}, {{ selectedUser.zipcode }}
            </div>
            <div class="pb-2">
              {{ selectedUser.state }}
            </div>
            <div class="pb-2">
              {{ selectedUser.country }}
            </div>
          </div>
        </div>

        <!-- <div class="mt-4">
          <iframe
            width="100%"
            height="300"
            :src="getGoogleMapsEmbedUrl(selectedUser.latitude, selectedUser.longitude)"
            frameborder="0"
            style="border:0"
            allowfullscreen=""
            loading="lazy"
          ></iframe>
        </div> -->
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    isVisible: {
      type: Boolean,
    },
    selectedUser: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    setNama(data) {
      const first_name = data.first_name;
      const last_name = data.last_name;
      return first_name + ' ' + last_name;
    },
    formatDate(dateString) {
      const options = { year: 'numeric', month: '2-digit', day: '2-digit' };
      const formattedDate = new Date(dateString).toLocaleDateString(undefined, options);
      return formattedDate;
    },
    closeModal() {
      this.$emit('close');
    },
    // getGoogleMapsEmbedUrl(latitude, longitude) {
    //   const apiKey = 'YOUR_GOOGLE_MAPS_API_KEY'; 
    //   const embedUrl = `https://www.google.com/maps/embed/v1/view?key=${apiKey}&center=${latitude},${longitude}&zoom=15`;
    //   return embedUrl;
    // },
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
