<template>
    <div>
        <md-toolbar>
            <h3 class="md-title">Random Amazon Ranking</h3>
            <div class="md-toolbar-section-end">
                <link rel="stylesheet"
                      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
                <a target="_blank" href="https://github.com/Silver-birder/amazon-ranking-vue">
                    <md-icon class="fa fa-github"></md-icon>
                </a>
            </div>
        </md-toolbar>
        <div v-show="loading" class="loader">Loading...</div>
        <div v-show="!loading">
            <md-card v-for="item in items">
                <img :src="item.crown">
                <md-card-media md-ratio="16:9">
                    <a target="_blank" :href="item.link">
                        <img :src="item.src" :alt="item.title">
                    </a>
                </md-card-media>
                <md-card-header>
                    <div class="md-title">{{item.title}}</div>
                </md-card-header>
                <md-card-content>
                    カテゴリ:
                    <a target="_blank" :href="item.url">
                        <div class="md-headline">{{item.category}}</div>
                    </a>
                </md-card-content>
            </md-card>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'AmazonRanking',
        data() {
            return {
                APP_AMAZON_RANKING_API: process.env.VUE_APP_AMAZON_RANKING_API,
                items: [],
                loading: true
            }
        },
        created() {
            for (let i = 0; i < 3; i++) {
                const random = Math.random().toString(36).slice(-8)
                this.axios
                    .get(`${this.APP_AMAZON_RANKING_API}/?r=${random}`)
                    .then(response => {
                        let items = response.data.data.items
                        items = items.map(item => {
                            item['url'] = response.data.data.url
                            item['category'] = response.data.data.category
                            return item
                        })
                        this.items = this.items.concat(items)
                        this.loading = false
                    })
                    .catch(response => {
                        alert("Not Data")
                    })
            }
        }
    }
</script>

<style>
    .card-expansion {
        height: 320px;
    }

    .md-card {
        width: 280px;
        margin: 4px;
        display: inline-block;
        vertical-align: top;
    }

    .loader,
    .loader:before,
    .loader:after {
        border-radius: 50%;
    }

    .loader {
        color: #ffffff;
        font-size: 11px;
        text-indent: -99999em;
        margin: 55px auto;
        position: relative;
        width: 10em;
        height: 10em;
        box-shadow: inset 0 0 0 1em;
        -webkit-transform: translateZ(0);
        -ms-transform: translateZ(0);
        transform: translateZ(0);
    }

    .loader:before,
    .loader:after {
        position: absolute;
        content: '';
    }

    .loader:before {
        width: 5.2em;
        height: 10.2em;
        background: #0dc5c1;
        border-radius: 10.2em 0 0 10.2em;
        top: -0.1em;
        left: -0.1em;
        -webkit-transform-origin: 5.2em 5.1em;
        transform-origin: 5.2em 5.1em;
        -webkit-animation: load2 2s infinite ease 1.5s;
        animation: load2 2s infinite ease 1.5s;
    }

    .loader:after {
        width: 5.2em;
        height: 10.2em;
        background: #0dc5c1;
        border-radius: 0 10.2em 10.2em 0;
        top: -0.1em;
        left: 5.1em;
        -webkit-transform-origin: 0px 5.1em;
        transform-origin: 0px 5.1em;
        -webkit-animation: load2 2s infinite ease;
        animation: load2 2s infinite ease;
    }

    @-webkit-keyframes load2 {
        0% {
            -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
        }
        100% {
            -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
        }
    }

    @keyframes load2 {
        0% {
            -webkit-transform: rotate(0deg);
            transform: rotate(0deg);
        }
        100% {
            -webkit-transform: rotate(360deg);
            transform: rotate(360deg);
        }
    }
</style>