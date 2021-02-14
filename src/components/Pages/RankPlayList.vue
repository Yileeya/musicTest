<template>
    <div class="row">
        <div class="col-md-12"><h3 class="header-title">KKBOX 排行榜</h3></div>
        <div class="col-md-12 text-center">
            <swiper :options="swiperOption">
                <swiper-slide v-for="(item, index) in rankList" :key="index">
                    <div @click="playMusic(item)">
                        <img class="img-thumbnail" :src="item.images[0].url"/>
                        <h5><b>{{ item.title }}</b></h5>
                    </div>
                </swiper-slide>
                <div class="swiper-button-prev" slot="button-prev">
                    <i class="fa fa-caret-left fa-5x" aria-hidden="true"></i>
                </div>
                <div class="swiper-button-next" slot="button-next">
                    <i class="fa fa-caret-right fa-5x" aria-hidden="true"></i>
                </div>
            </swiper>
        </div>
    </div>
</template>

<script>
    import {mapActions, mapGetters} from 'vuex';
    import axios from 'axios';

    export default {
        name: "RankPlayList",
        computed: {
            ...mapGetters(['kkboxToken', 'AJAXConfig'])
        },
        data() {
            return {
                rankList: [],
                swiperOption: {
                    slidesPerView: 5,//單排數量
                    loop: true,
                    autoplay: {
                        delay: 6000,
                        disableOnInteraction: false
                    },
                    navigation: {
                        nextEl: '.swiper-button-next',
                        prevEl: '.swiper-button-prev'
                    },
                    breakpoints://RWD決定單排數量
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
            this.getRanking();
        },
        methods: {
            ...mapActions(['getToken']),
            async getRanking() {
                const rankPlaylistUrl = `https://api.kkbox.com/v1.1/charts?territory=TW`;
                let res = await axios.get(rankPlaylistUrl, this.AJAXConfig);
                res = res.data;
                this.rankList = res.data;
            },
            playMusic(item) {
                this.$emit('Charts', item);
            }
        }
    }
</script>

<style scoped>
    .img-thumbnail{
        width: 90%;
    }
    .swiper-button-prev, .swiper-button-next{
        top: 40% !important;
    }
</style>