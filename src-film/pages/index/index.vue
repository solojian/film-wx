<template>
  <div >
    hello mpvue
    <ul>
      <li v-for="item in dataList" :key="item.filmId" @click="handle(item.filmId)">
        <image :src='item.poster' mode="widthFix"/>
        <div class="right">
          <h2>{{item.name}} </h2>
          <p>观众评分：{{item.grade}}</p>
          <p>主演：<span v-for="(actor,acindex) in item.actors" :key="acindex">{{actor.name}}</span></p>
          <p>{{item.nation}}|{{runtime}}分钟</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  data () {
    return {
      dataList: [],
      current: 1
    }
  },
  created () {
    if (mpvuePlatform === 'wx') {
      mpvue.request({
        url: 'https://m.maizuo.com/gateway?cityId=110100&pageNum=1&pageSize=10&type=1&k=8280865',
        header: {
          'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1597714209564019400278017","bc":"110100"}',
          'X-Host': 'mall.film-ticket.film.list'
        },
        success: (res) => {
          console.log(res.data)
          this.dataList = res.data.data.films
        }
      })
    }
    // let app = getApp()
  },
  methods: {
    handle (id) {
      console.log(id)
      mpvue.navigateTo({
        url: '/pages/details/main?id=' + id
      })
    }
  },
  onPullDownRefresh () {
    console.log('xialale')
    setTimeout(() => {
      mpvue.stopPullDownRefresh()
    }, 1000)
  },
  onReachBottom () {
    console.log('daodile')
    this.current++
    if (mpvuePlatform === 'wx') {
      mpvue.request({
        url: `https://m.maizuo.com/gateway?cityId=110100&pageNum=${this.current}&pageSize=10&type=1&k=8280865`,
        header: {
          'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1597714209564019400278017","bc":"110100"}',
          'X-Host': 'mall.film-ticket.film.list'
        },
        success: (res) => {
          console.log(res.data)
          this.dataList = [...this.dataList, ...res.data.data.films]
        }
      })
    }
  }
}
</script>

<style scoped lang='scss'>
  ul {
    li {
      padding: 15px 15px 15px 0;
      overflow: hidden;
      image {
        padding: 8px;
        width: 100px;
        float: left;
      }
      .right {
        overflow: hidden;
        h2 {
          margin: 12px 0;
          height: 22px;
          line-height: 22px;
          width: 100%;
          font-size: 18px;
        }
        p {
          width: 100%;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
          font-size: 15px;
          color: #797d82;
          margin: 8px 0;
        }
      }
    }
  }
</style>
