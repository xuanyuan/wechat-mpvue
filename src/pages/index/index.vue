<template>
  <div class="container">
    <mp-searchbar :value="inputValue"
                  :placeholder="搜索"
                  confirmType="search"
                  @confirm="requesttest">
    </mp-searchbar>
    <mp-grid :gridData="gridData"></mp-grid>
    <div class="weui-cells weui-cells_after-title">
      <!-- <div class="weui-cell weui-cell_access">
        <div class="weui-cell__bd">
          <div class="single-line">单行列表</div>
          <div class="weui-badge">8</div>
        </div>
        <a href="../counter/main"
           class="weui-cell_ft weui-cell__ft_in-access">详细信息</a>
      </div> -->
      <div class="weui-cell weui-cell_access">
        <div class="weui-cell__bd">
          <div class="single-line">单行列表</div>
          <div class="weui-badge">New</div>
        </div>
        <a href="../counter/main"
           class="weui-cell_ft weui-cell__ft_in-access">
        </a>
      </div>
    </div>
    <!-- 加载进度框 -->
    <mp-loading :showLoading="isShowLoading"
                loadingText="玩命加载中"
                :mask="isShowMask"></mp-loading>

  </div>
</template>
<script>
import mpSearchbar from 'mpvue-weui/src/searchbar'
import mpGrid from 'mpvue-weui/src/grid'
import mpLoading from 'mpvue-weui/src/loading'
import mpBadge from 'mpvue-weui/src/badge'
import Fly from 'flyio/dist/npm/wx'

export default {
  data () {
    return {
      inputValue: '',
      isShowLoading: false,
      isShowMask: false,
      gridData: [
        {
          src: '/static/images/chuzu.png',
          name: '出租',
          url: '../lease/main'
        },
        {
          src: '/static/images/yiliao.png',
          name: '医疗',
          url: '../treatment/main'
        },
        {
          src: '/static/images/fangchan.png',
          name: '办证',
          url: '../certificates/main'
        }
      ]
    }
  },

  components: {
    mpBadge,
    mpGrid,
    mpLoading,
    mpSearchbar
  },

  methods: {
    bindViewTap () {
      console.log('sdssf')
      const url = '@/pages/logs/main'

      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    requesttest () {
      var self = this
      this.isShowLoading = true
      let fly = new Fly()
      fly.get('https://mp.miaodongshequ.com/')
        .then((res) => {
          this.isShowLoading = false
          console.log(res.data)
        })
        .catch((err) => {
          this.isShowLoading = false
          self.list = err
        })
    }
  },

  created () {
  }
}
</script>

<style scoped>
.badge-box {
  border-top: 1rpx solid #ccc;
  border-bottom: 1rpx solid #ccc;
  margin: 10rpx 0;
  position: relative;
}
.single-line {
  display: inline-block;
  vertical-align: middle;
}
</style>
