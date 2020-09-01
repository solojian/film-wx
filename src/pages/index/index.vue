<template>
    <div class="index_container">
        <img :src="userinfo.avatarUrl" alt="" class="index_img" v-if="isShow">
        <Button open-type='getUserInfo' @getuserinfo='getUserInfo' v-else>点击获取用户信息</Button>
        <p class="username">hello {{userinfo.nickName}}</p>
        <div class="gostudy" @click="toDetails">
            <p>开启小程序之旅</p>
        </div>
    </div>
</template>
<script>
export default {
  data () {
    return {
        userinfo: {},
        isShow: false
    }
  },
//   mounted() {
//       this.handleGet()
//   },
  methods: {
    handleGet() {
              wx.getUserInfo({
                  success: (data) => {
                    console.log(data)
                    this.userinfo = data.userInfo
                    this.isShow = true
                  },
                  fail: () => {
                      console.log('err massage')
                  }
              }) 
          },
    getUserInfo(data) {
        if(data.mp.detail.rawData) {
            this.handleGet()
        }
    },
    toDetails() {
        wx.navigateTo({
            url: '/pages/details/main'
        })
    }
  }
}
</script>
<style lang="scss" scoped>
    page {
        background-color: #8ed145;
    }
    .index_container {
        display: flex;
        flex-direction: column;
        align-items: center;
        img {
            width: 200rpx;
            height: 200rpx;
            border-radius: 100rpx;
            margin: 100rpx 0;
        }
        .username {
            font-size: 40rpx;
            margin: 60rpx 0;
            font-weight: bold;
        }
        .gostudy {
            border: 1rpx solid #eee;
            width: 200rpx;
            height: 80rpx;
            line-height: 80rpx;
            font-size: 24rpx;
            border-radius: 8rpx;
            text-align: center;
        }
    }
</style>