<template>
  <div class="container mx-auto px-8 my-8">
    <Table :data="tableData" />
  </div>
</template>

<script>
import Table from "../components/TableProvince.vue";
import provinces from '../assets/js/province';

export default {
  components: {
    Table
  },
  data() {
    return {
      tableData: provinces,
    };
  },
  mounted () {
  },
  methods: {
  }
};
</script>

<style scoped>
</style>
