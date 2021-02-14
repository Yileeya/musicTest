<template>
    <div class="blue row">




<!--        <iframe width="775" height="600" src="https://widget.kkbox.com/v1/?id=4nNhQdTo2aVxaakNY6&amp;type=playlist&amp;terr=tw&amp;lang=tc" frameborder="0" scrolling="no"></iframe>-->


<!--        <iframe width="775" height="600" src="https://widget.kkbox.com/v1/?id=KsOjSf4whgbL45hRfl&amp;type=playlist&amp;terr=tw&amp;lang=tc" frameborder="0" scrolling="no"></iframe>-->

<!--        <iframe src="https://widget.kkbox.com/v1/?id=GonWvutNzZWl9MKBmf&type=album&terr=SG&lang=en&autoplay=true" allow="autoplay"></iframe>-->
        <iframe width="775" height="1600" :src="`https://widget.kkbox.com/v1/?id=GrtWTdwZSVBLbTK2rG&type=album&terr=TW&lang=TC`"/>


        <div class="col-md-3">1</div>
        <div class="col-md-3">2</div>
        <div class="col-md-3">3</div>
        <div class="col-md-3">4</div>
        <!--    <h1>{{ msg }}</h1>-->
        <!--    <p>-->
        <!--      For a guide and recipes on how to configure / customize this project,<br>-->
        <!--      check out the-->
        <!--      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.-->
        <!--    </p>-->
        <!--    <h3>Installed CLI Plugins</h3>-->
        <!--    <ul>-->
        <!--      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>-->
        <!--      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>-->
        <!--    </ul>-->
        <!--    <h3>Essential Links</h3>-->
        <!--    <ul>-->
        <!--      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>-->
        <!--      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>-->
        <!--      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>-->
        <!--      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>-->
        <!--      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>-->
        <!--    </ul>-->
        <!--    <h3>Ecosystem</h3>-->
        <!--    <ul>-->
        <!--      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>-->
        <!--      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>-->
        <!--      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>-->
        <!--      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>-->
        <!--      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>-->
        <!--    </ul>-->
    </div>
</template>

<script>
    import qs from 'querystring';
    import axios from 'axios';

    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                token: null,
                song:[]
            }
        },
        created() {
            this.getToken();
        },
        methods: {
            async getToken() {
                const config = {
                    headers: {
                        Accept: 'application/x-www-form-urlencoded',
                        'Content-Type': 'application/x-www-form-urlencoded'
                    }
                };
                const oauth = {
                    grant_type: 'client_credentials',
                    client_id: '32d6e6eed3e5c2da1c9b4c48fb2542b0',
                    client_secret: 'a45b2b68c98164d6bc89f1dc4918e6f6'
                };
                let res = await axios.post('/token', qs.stringify(oauth), config);
                res = res.data;
                this.token = res.access_token;
                this.search()
            },
            async search(){
                let res = await axios.get('https://api.kkbox.com/v1.1/search?q=郭靜&type=artist,track&territory=TW',{
                    headers: {
                        'Authorization': `Bearer ${this.token}`
                    }
                })
                res = res.data;
                this.song = res;
                // this.song = res.tracks.data[0].id
                // this.$http.get('https://api.kkbox.com/v1.1/search?q=盧芸&type=artist,track&territory=TW', config)
                // GET v1.1/search?q=盧芸&type=artist,track&territory=TW HTTP/1.1
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3{
        margin: 40px 0 0;
    }
    ul{
        list-style-type: none;
        padding:         0;
    }
    li{
        display: inline-block;
        margin:  0 10px;
    }
    a{
        color: #42b983;
    }

</style>
