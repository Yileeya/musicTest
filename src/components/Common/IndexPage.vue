<template>
    <div>
        <div class="img-fluid" alt="Responsive image"></div>
        <div style="background: white">
            <hot-play-list @Charts="playMusic"></hot-play-list>
            <style-list-page></style-list-page>
            <rank-play-list @Charts="playMusic"></rank-play-list>
        </div>
        <template v-if="musicAutoplay">
            <play-list-modal @autoPlay="AutoPlay" v-model="modal.show" :musicSrc="musicObject"></play-list-modal>
        </template>
    </div>
</template>

<script>
    import HotPlayList from '@/components/Pages/HotPlayList';
    import PlayListModal from '@/components/Common/PlayListModal';
    import RankPlayList from '@/components/Pages/RankPlayList';
    import StyleListPage from '@/components/Pages/StyleListPage';

    export default {
        name: "IndexPage",
        components: {StyleListPage, RankPlayList, PlayListModal, HotPlayList},
        data() {
            return {
                musicObject: {
                    id: 'DZrC8m29ciOFY2JAm3',
                    type: 'playlist',
                    autoplay: false
                },
                modal: {
                    show: false
                },
                musicAutoplay: false
            };
        },
        methods: {
            playMusic(item) {
                this.musicObject = item;
                this.musicObject.type = 'playlist';
                this.musicObject.autoplay = true;

                this.musicAutoplay = true;
                this.modal.show = true;
            },
            AutoPlay() {
                this.musicAutoplay = false;
            }
        }
    }
</script>

<style scoped>
    .img-fluid{
        height:                250px;
        background-color:      #A6808C;
        opacity:               0.6;
        background-blend-mode: multiply;
        background-image:      url(https://www.emome.net/files/fckeditor/image/images/bn/bn-service-small-8.jpg);
        background-size:       cover;
        background-position:   center center;
    }
</style>