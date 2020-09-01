<template>
<div></div>
</template>
<script>
export default {
  data () {
    return {
    }
  },
//   onLoad (options) {
//       console.log(options)
//   }
    mounted () {
       console.log(this.$root.$mp.query)
        if (mpvuePlatform === 'wx') {
        mpvue.request({
          url: `https://m.maizuo.com/gateway?filmId=${this.$root.$mp.query}&k=6883125`,
          header: {
           ' X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1597714209564019400278017","bc":"110100"}',
            'X-Host': 'mall.film-ticket.film.info'
          },
          success: (res) => {
            console.log('res.data')
          }
        })
      }
 }
}
</script>
<style lang="css" scoped>
</style>