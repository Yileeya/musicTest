<template>
    <div class="row">
        <div class="col-md-12"><h3 class="header-title">KKBOX 風格清單</h3></div>
        <div class="col-md-12 text-center">
            <swiper :options="swiperOption">
                <swiper-slide class="swiper-style img-thumbnail" v-for="(item, index) in styleList" :key="index.id">
                    <div @click="test">
                        <h4><b>{{ item.title }}</b></h4>
                    </div>

                    <!--                <router-link class="text-decoration" :to="`/categories/${item.id}`">-->
                    <!--                    <div class="style-box">-->
                    <!--                        <p class="font-weight-bold m-0">♫ {{ item.title }}</p>-->
                    <!--                    </div>-->
                    <!--                </router-link>-->
                </swiper-slide>
                <div class="swiper-button-prev" slot="button-prev">
                    <i style="color: white" class="fa fa-caret-left fa-3x" aria-hidden="true"></i></div>
                <div class="swiper-button-next" slot="button-next"><i style="color: white" class="fa fa-caret-right fa-3x" aria-hidden="true"></i></div>
            </swiper>
        </div>
    </div>
</template>

<script>
    import {mapActions, mapGetters} from 'vuex';
    import axios from 'axios';

    export default {
        name: "StyleListPage",
        computed: {
            ...mapGetters(['kkboxToken', 'AJAXConfig'])
        },
        data() {
            return {
                styleList: [],
                swiperOption: {
                    slidesPerView: 4,
                    spaceBetween: 5,
                    loop: true,
                    autoplay: {
                        delay: 5000,
                        disableOnInteraction: false
                    },
                    navigation: {
                        nextEl: '.swiper-button-next',
                        prevEl: '.swiper-button-prev'
                    },
                    breakpoints:
                        {
                            992: {
                                slidesPerView: 3
                            },
                            768: {
                                slidesPerView: 2
                            },
                            576: {
                                slidesPerView: 2
                            }
                        }
                }
            }
        },
        async created() {
            await this.getToken();
            this.getStyleList();
        },
        methods: {
            ...mapActions(['getToken']),
            async getStyleList() {
                let res = await axios.get(`https://api.kkbox.com/v1.1/new-release-categories?territory=TW`, this.AJAXConfig);
                res = res.data;
                this.styleList = res.data;
            },
            async test() {
                await axios.get(`https://api.kkbox.com/v1.1/new-release-categories/1ZQwmFTaLE4p7BG-Ua?territory=TW`, this.AJAXConfig);
                // HaGEkt7m7GQpGZOizF
                // this.$http.get(`${process.env.VUE_APP_KKBOXURL}/new-release-categories/${this.categoriesid}?territory=TW`, this.AJAXConfig)
                //     .then((res) => {
                //         this.categoriesData = res.data;
                //         this.$store.commit('LOADING', false);
                //     });

            }
        }
    }
</script>

<style scoped lang="scss">
    .swiper-style{
        padding:       0;
        border-radius: 10px;
        height:        200px;
        &:nth-child(4n){
            background-image:    url("https://image.freepik.com/free-photo/large-diaphragm-condenser-microphone-with-musician-holding-electric-guitar-backgroun_181624-3844.jpg");
            background-size:     cover;
            background-position: center;
        }
        &:nth-child(4n+1){
            background-image:    url("https://image.freepik.com/free-photo/woman-headphones-recording-music_155003-16942.jpg");
            background-size:     cover;
            background-position: center;
        }
        &:nth-child(4n+2){
            background-image:    url("https://image.freepik.com/free-photo/closeup-shot-microphone-blurred-space-with-bokeh-lights_181624-24707.jpg");
            background-size:     cover;
            background-position: center;
        }
        &:nth-child(4n+3){
            background-image:    url("https://image.freepik.com/free-photo/side-view-woman-singing-microphone_141793-14270.jpg");
            background-size:     cover;
            background-position: center;
        }
        h4{
            display:         flex;
            justify-content: center;
            align-items:     center;
            height:          220px;
            background:      rgba(0, 0, 0, 0.5);
            border-radius:   10px;
            color:           white;
            letter-spacing:  1rem;
            margin:          0;
        }
        .img-thumbnail{
            padding: 0;
        }
    }
</style>