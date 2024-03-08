<template>
    <div class="container mt-5" v-if="schoolprofile">
        <section class="section about-section gray-bg" id="about">
            <div class="container">
                <div class="row align-items-center flex-row-reverse">
                    <div class="col-lg-6">
                        <div class="about-text go-to">
                            <h3 class="dark-color">{{schoolprofile.name}}</h3>
                            <h6 class="theme-color lead">{{schoolprofile.address.area}},
                                {{schoolprofile.address.city.name}}
                            </h6>
    
                            <p>{{plainText}}...</p>
                            <div class="row about-list">
                                <div class="col-md-6">
                                    <div class="media">
                                        <label>Year Estd</label>
                                        <p>{{schoolprofile.year_of_establishment}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Format</label>
                                        <p>{{schoolprofile.format}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Level</label>
                                        <p>{{schoolprofile.level}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Classes</label>
                                        <p>{{schoolprofile.classes_offered}}</p>
                                    </div>
                                </div>
                                <div class="col-md-6">
                                    <div class="media">
                                        <label>Coed</label>
                                        <p>{{schoolprofile.coed_status}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Ownership</label>
                                        <p>{{schoolprofile.ownership}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Session</label>
                                        <p>{{schoolprofile.academic_session}}</p>
                                    </div>
                                    <div class="media">
                                        <label>Medium</label>
                                        <p>{{schoolprofile.medium}}</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="about-avatar">
                            <img :src="schoolprofile.logo" title="" alt="">
                        </div>
                    </div>
                </div>
                <div class="counter">
                    <div class="row">
                        <div class="col-6 col-lg-3">
                            <div class="count-data text-center">
                                <h6 class="count h2" data-to="500" data-speed="500">{{schoolprofile.boards[0]}}</h6>
                                <p class="m-0px font-w-600">Boards</p>
                            </div>
                        </div>
                        <div class="col-6 col-lg-3">
                            <div class="count-data text-center">
                                <h6 class="count h2" data-to="150" data-speed="150">{{schoolprofile.views}}</h6>
                                <p class="m-0px font-w-600">School Views</p>
                            </div>
                        </div>
                        <div class="col-6 col-lg-3">
                            <div class="count-data text-center">
                                <h6 class="count h2" data-to="850" data-speed="850">{{schoolprofile.verified_by_school}}
                                </h6>
                                <p class="m-0px font-w-600">Application Partner</p>
                            </div>
                        </div>
                        <div class="col-6 col-lg-3">
                            <div class="count-data text-center">
                                <h6 class="count h2" data-to="190" data-speed="190">{{schoolprofile.verified_by_school}}
                                </h6>
                                <p class="m-0px font-w-600">Verified By School</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
    <div v-else>
        <NuxtLoadingIndicator />
    </div>
</template>

<script>
import axios from "axios";
import he from "he";


export default {
  data() {
    return {
      schoolprofile: undefined, plainText: undefined
    }
  },
  async mounted() {
    this.fetchSchoolProfile();
  },
  methods: {
    async fetchSchoolProfile() {
      const slug = this.$route.params.slug;
      try {
        const res = await axios.get(`https://api.main.ezyschooling.com/api/v3/schools/${slug}`)
        this.schoolprofile = res.data
        const html = this.schoolprofile.about;
        const decodedPlainText = he.decode(html);
        this.plainText = decodedPlainText.replace(/<[^>]+>/g, '').substring(0, 200);
        console.log(this.plainText);
      } catch (error) {
        console.error(error);
      }
    }
  }

}
</script>
<style scoped>
body {
    color: #6F8BA4;
    margin-top: 20px;
}

.section {
    padding: 100px 0;
    position: relative;
}

.gray-bg {
    background-color: #f5f5f5;
}

img {
    mix-blend-mode: multiply;
    min-width: 500px;
    min-height: 500px;
    max-width: 100%;
}

img {
    vertical-align: middle;
    border-style: none;
}

/* About Me 
---------------------*/
.about-text h3 {
    font-size: 45px;
    font-weight: 700;
    margin: 0 0 6px;
}

@media (max-width: 767px) {
    .about-text h3 {
        font-size: 35px;
    }
}

.about-text h6 {
    font-weight: 600;
    margin-bottom: 15px;
}

@media (max-width: 767px) {
    .about-text h6 {
        font-size: 18px;
    }
}

.about-text p {
    font-size: 18px;
    max-width: 450px;
}

.about-text p mark {
    font-weight: 600;
    color: #20247b;
}

.about-list {
    padding-top: 10px;
}

.about-list .media {
    padding: 5px 0;
}

.about-list label {
    color: #20247b;
    font-weight: 600;
    width: 88px;
    margin: 0;
    position: relative;
}

.about-list label:after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    right: 13px;
    width: 1px;
    height: 12px;
    background: #20247b;
    -moz-transform: rotate(15deg);
    -o-transform: rotate(15deg);
    -ms-transform: rotate(15deg);
    -webkit-transform: rotate(15deg);
    transform: rotate(15deg);
    margin: auto;
    opacity: 0.5;
}

.about-list p {
    margin: 0;
    font-size: 15px;
}

@media (max-width: 991px) {
    .about-avatar {
        margin-top: 30px;
    }
}

.about-section .counter {
    padding: 22px 20px;
    background: #ffffff;
    border-radius: 10px;
    box-shadow: 0 0 30px rgba(31, 45, 61, 0.125);
}

.about-section .counter .count-data {
    margin-top: 10px;
    margin-bottom: 10px;
}

.about-section .counter .count {
    font-weight: 700;
    color: #20247b;
    margin: 0 0 5px;
}

.about-section .counter p {
    font-weight: 600;
    margin: 0;
}

mark {
    background-image: linear-gradient(rgba(252, 83, 86, 0.6), rgba(252, 83, 86, 0.6));
    background-size: 100% 3px;
    background-repeat: no-repeat;
    background-position: 0 bottom;
    background-color: transparent;
    padding: 0;
    color: currentColor;
}

.theme-color {
    color: #fc5356;
}

.dark-color {
    color: #20247b;
}
</style>