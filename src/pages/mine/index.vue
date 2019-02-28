<template>
  <div>
    <div class="userinfo"
         v-if="userInfo.nickName">
      <img class="userinfo-avatar"
           :src="userInfo.avatarUrl"
           v-if="userInfo.avatarUrl"
           background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>
    <button v-if="!userInfo.nickName"
            open-type="getUserInfo"
            @getuserinfo="authSetUser">
      授权登录
    </button>

    <div class="weui-cells weui-cells_after-title">
      <div class="weui-cell weui-cell_access">
        <div class="weui-cell__bd">
          <div class="single-line">资料修改</div>
        </div>
        <a href="../counter/main"
           class="weui-cell_ft weui-cell__ft_in-access">
        </a>
      </div>
    </div>
    <div class="weui-cells weui-cells_after-title">
      <div class="weui-cell weui-cell_access">
        <div class="weui-cell__bd">
          <div class="single-line">留言反馈</div>
        </div>
        <a href="../counter/main"
           class="weui-cell_ft weui-cell__ft_in-access">
        </a>
      </div>
    </div>
  </div>
</template>
<script>
import card from '@/components/card'
export default {
  data () {
    return {
      userInfo: {}
    }
  },
  components: {
    card
  },
  created () {
    this.getUserInfo()
  },
  methods: {
    authSetUser (e) {
      this.userInfo = e.mp.detail.userInfo
    },
    getUserInfo () {
      // 调用登录接口
      var _this = this
      wx.getUserInfo({// 当已授权getUserInfo时
        success (res) {
          console.log(res)
          _this.userInfo = res.userInfo
        },
        fail (err) {
          console.log(err)
        }
      })
    }
  }
}
</script>
<style>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}
</style>

