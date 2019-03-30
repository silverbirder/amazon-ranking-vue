<template>
  <div class="hello">
  </div>
</template>

<script>
export default {
  name: 'AmazonRanking',
  data () {
      // console.log(process.env.VUE_APP_AMAZON_RANKING_API)
      // this.axios.get(process.env.VUE_APP_AMAZON_RANKING_API).then(response => {
      //     console.log(response)
      // })
      const response = {
          data: [],
          message: '',
          url: '',
      }
      return {
          'APP_AMAZON_RANKING_API': process.env.VUE_APP_AMAZON_RANKING_API,
      }
  },
  methods: {
      // onUpdate: function() {
      //     this.axios.get(this.APP_AMAZON_RANKING_API)
      // }
  }
}
</script>
