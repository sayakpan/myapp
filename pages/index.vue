<template>
  <div class="container">
    <h4>Most Applied Schools</h4>
    <p>Apply to our parent's top applied schools</p>
    <div class="container text-center mt-5">
      <div class="row g-1 mt-5">
        <SchoolCard v-for="school in schoollist" :slug="school.slug" :key="school.id" :school="school"></SchoolCard>
      </div>
      <div class="mt-3 d-flex align-items-center justify-content-center">
        <pagination v-model="page" :records="totalSchools" :per-page="perPage" @paginate="onPageChange" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SchoolCard from '../components/SchoolCard.vue';
import Pagination from "vue-pagination-2";


export default {
  components: { SchoolCard, Pagination },
  name: 'IndexPage',
  data() {
    return {
      page: 1,
      schoollist: [],
      totalSchools: 0,
      perPage: 20 // Number of schools per page
    }
  },
  async created() {
    this.fetchSchools();
  },
  methods: {
    onPageChange() {
      this.fetchSchools()
    },
    async fetchSchools() {
      const config = {
        params: {
          limit: this.perPage,
          active: true,
          verified: true,
          offset: (this.page - 1) * this.perPage,
          school_city: '',
          ordering: ['-global_rank', '-region_rank', '-collab', '-non_collab_form_filling', '-admissionclasses_open_count', '-total_views']
        }
      }
      try {
        const res = await axios.get("https://api.main.ezyschooling.com/api/v1/schools/document/", config);
        this.schoollist = res.data.results;
        this.totalSchools = res.data.count;
      } catch (error) {
        console.error(error);
      }
    },
    onPageChange(page) {
      this.page = page;
      this.fetchSchools();
    }
  }
}
</script>
<style scoped>

</style>