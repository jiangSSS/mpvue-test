<template>
  <div class="container">
    <img v-if="!isShow" class="user-avatar" :src="userInfo.avatarUrl" alt="">
    <Button v-else open-type="getUserInfo" @getuserInfo="getUserInfo">获取用户信息</Button>
    <p class="userName">hello {{userInfo.nickName}}</p>
    <div>
      <p class="go">进入周刊</p>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        userInfo: {},
        isShow:false,     // 表示用户没有授权
      }
    },
    beforeMount(){
      this.handleGetUserInfo()
    },
    methods: {
      // 获取用户登录信息
      handleGetUserInfo() {
        wx.getUserInfo({
          success: (data) => {
            console.log(data)
            this.userInfo = data.userInfo
          },
          fail: () => {
            console.log("获取失败")
          }
        })
      },
      getUserInfo(data) {
        // 判断用户是否授权
        if (data.mp.detail.rawData) {
          this.handleGetUserInfo()
        }
      }
    }
  }
</script>

<style>
  page {
    background: #81d145;
  }

  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .user-avatar {
    width: 200rpx;
    height: 200rpx;
    margin: 100rpx 0;
    border-radius: 50%;
  }

  .userName {
    font-size: 40rpx;
    font-weight: bold;
    margin: 100rpx 0;
    color: #fff;

  }

  .go {
    width: 220rpx;
    height: 80rpx;
    text-align: center;
    line-height: 80rpx;
    border: 1rpx solid #eee;
    color: #fff;
    border-radius: 10rpx;
  }

  .usermotto {
    margin-top: 150px;
  }

  .form-control {
    display: block;
    padding: 0 12px;
    margin-bottom: 5px;
    border: 1px solid #ccc;
  }

  .counter {
    display: inline-block;
    margin: 10px auto;
    padding: 5px 10px;
    color: blue;
    border: 1px solid blue;
  }
</style>