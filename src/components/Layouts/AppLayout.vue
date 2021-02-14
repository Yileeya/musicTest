<template>
    <div class="row" style="background: rgba(166, 128, 140, 0.8)">
        <div class="col-md-2">
            <header-view @TT="jump"></header-view>
        </div>
        <div class="col-md-10">
            <index-page></index-page>
        </div>
    </div>
</template>

<script>
    import HeaderView from '@/components/Common/HeaderView';
    import IndexPage from '@/components/Common/IndexPage';

    export default {
        name: "AppLayout",
        components: {IndexPage, HeaderView},
        data() {
            return {
                TT: null
            }
        },
        watch: {
            TT() {
                this.jump()
            }
        },
        methods: {
            jump() {
                // alert()
                let scrollDiv = document.getElementById("one").offsetTop;
                window.scrollTo({ top: scrollDiv, behavior: 'smooth'});



                // document.getElementById(`one`).scrollIntoView({
                //     behavior: "smooth" // 平滑过渡
                // })
            }
        }
    }
</script>

<style lang="scss" scoped>
    .col-md-2{
        padding: 0;
    }
    .col-md-10{
        padding: 0;
    }
</style>
