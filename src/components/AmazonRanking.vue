<template>
    <div>
        <a target="_blank" :href="data.url">
            <div class="md-headline">{{data.category}}</div>
        </a>
        <md-card v-for="item in data.items">
            <img :src="item.crown">
            <md-card-media md-ratio="16:9">
                <a target="_blank" :href="item.link">
                    <img :src="item.src" :alt="item.title">
                </a>
            </md-card-media>
            <md-card-header>
                <div class="md-title">{{item.title}}</div>
            </md-card-header>
        </md-card>
    </div>
</template>

<script>
    export default {
        name: 'AmazonRanking',
        data() {
            return {
                APP_AMAZON_RANKING_API: process.env.VUE_APP_AMAZON_RANKING_API,
                data: {
                    url: '',
                    category: '',
                    items: []
                }
            }
        },
        created() {
            console.log(this.APP_AMAZON_RANKING_API)
            this.axios
                .get(this.APP_AMAZON_RANKING_API)
                .then(response => {
                    this.data = response.data.data
                })
                .catch(response => {
                    alert("Not Fetch")
                })
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
</style>