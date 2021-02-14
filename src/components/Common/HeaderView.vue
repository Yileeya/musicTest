<template>
    <div>
        <template>
            <div class="text-center">
                <i class="fa fa-music fa-4x" aria-hidden="true"></i>
            </div>
            <h4 class="text-center">F2E<br>x<br>KKBOX OPENAPI</h4>
        </template>
        <nav class="navbar bg-light">
            <ul class="nav navbar-nav">
                <li class="sub-title">
                    <a class="nav-link">
                        首頁
                    </a>
                </li>
                <li class="nav-item" v-for="item in navItemList" :key="item.id">
                    <a class="nav-link" @click="$emit('TT', 'one')"><h5>- {{ item.name }}</h5></a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script>
    export default {
        name: "HeaderView",
        data() {
            return {
                navItemList: [
                    {
                        id: 1,
                        name: '速爆新歌',
                        href: 'hot'
                    },
                    {
                        id: 2,
                        name: '風格清單',
                        href: 'style'
                    },
                    {
                        id: 3,
                        name: '排行榜',
                        href: 'rank'
                    }
                ]
            }
        }
    }
</script>

<style scoped>
    h4{
        padding: 0;
        margin:  0;
    }
    .fa-4x{
        background:    white;
        padding:       5% 7%;
        border-radius: 50px;
        margin:        0.25em 0;
        color:         #706677;
    }
    .sub-title{
        font-size:      20px;
        letter-spacing: 1rem;
        font-weight:    bold;
    }
    h5{
        font-size:      16px;
        margin:         0 1em;
        letter-spacing: 0.5rem;
        font-weight:    bold;
    }
    .bg-light{
        margin: 30px;
    }
    a{
        color: white !important;
    }
</style>