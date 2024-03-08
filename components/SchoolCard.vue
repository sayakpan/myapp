<template>
    <div class="col-md-12">
        <div class="card mb-3" style="max-height: 150px">
            <div class="row no-gutters">
                <div class="col-md-2">
                    <img :src="school.logo" class="card-img-top">
                </div>
                <div class="col-md-10">
                    <div class="card-body text-left">
                        <nuxt-link :to="'profile/'+slug">
                            <h5 class="card-title m-0 d-flex justify-content-between">{{school.name}}
                                <span v-if="school.collab" class="badge badge-success ">Application
                                    Partner</span>
                            </h5>
                        </nuxt-link>
    
                        <small>{{school.district_region.name}}, {{school.school_city.name}}</small>
                        <div class="d-flex justify-content-between">
                            <div class="mt-2">
                                <span class="item-label text-muted d-block small mr-0">Affiliated To</span>
                                <span class="item-val font-weight-semibold">{{school.school_board.name}}</span>
                            </div>
                            <div class="mt-2">
                                <span class="item-label text-muted d-block small mr-0">Average Monthly Fees</span>
                                <span class="item-val font-weight-semibold">Rs. {{school.max_fees}}</span>
                            </div>
                            <div class="mt-2">
                                <span class="item-label text-muted d-block small mr-0">Student Teacher Ratio</span>
                                <span class="item-val font-weight-semibold">{{school.student_teacher_ratio}}</span>
                            </div>
                            <div class="mt-2">
                                <span class="item-label text-muted d-block small mr-0">Year Estd.</span>
                                <span class="item-val font-weight-semibold">{{school.year_established}}</span>
                            </div>
                            <div class="mt-2">
                                <span class="item-label text-muted d-block small mr-0">School Category</span>
                                <span class="item-val font-weight-semibold">{{school.school_category}}</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "SchoolCard",
  props: ["school", 'slug']
}
</script>

<style scoped>
img {
    width: 146px;
    height: 146px;
    object-fit: contain;
}
</style>