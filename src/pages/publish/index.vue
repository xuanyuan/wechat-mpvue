<template>
  <div class="form">
    <div class="form-group">
      <label for="chooseCommunity">选择小区</label>
      <input type="text"
             disabled
             id="chooseCommunity"
             placeholder="点击选择小区"
             @click="showMulLinkageTwoPicker"
             v-model="community" />
    </div>
    <!-- 选择小区 -->
    <mp-picker ref="mpPicker"
               :mode="mode"
               :deepLength=deepLength
               :pickerValueDefault="pickerValueDefault"
               @onChange="onChange"
               @onConfirm="onConfirm"
               @onCancel="onCancel"
               :pickerValueArray="pickerValueArray"></mp-picker>
    <div class="form-group">
      <label for="">发布标题</label>
      <input type="text"
             maxlength="20"
             v-model="infotitle"
             placeholder="输入标题" />
    </div>

    <textarea name="发布信息"
              id=""
              v-model="content"
              rows="10"></textarea>
    <mp-uploader @uploadDelete="uploadDelete"
                 :showTip=true
                 :count=1
                 :maxLength=5
                 @upLoadSuccess="upLoadSuccess"></mp-uploader>
    <mp-button type="primary"
               size="normal"
               btnClass="mb"
               @click="sendPublishInfo">发布</mp-button>
  </div>

</template>
<script>
import mpPicker from 'mpvue-weui/src/picker'
import mpSearchbar from 'mpvue-weui/src/searchbar'
import mpButton from 'mpvue-weui/src/button'
import mpUploader from 'mpvue-weui/src/uploader'
import Fly from 'flyio/dist/npm/wx'

export default {
  components: {
    mpPicker,
    mpSearchbar,
    mpButton,
    mpUploader
  },
  data () {
    return {
      mode: 'multiLinkageSelector',
      pickerValueArray: [
        {
          label: '飞机票',
          value: 100,
          children: [
            {
              label: '经济舱',
              value: 101
            },
            {
              label: '商务舱',
              value: 102
            }
          ]
        }
      ],
      community: '',
      infotitle: '',
      pickerValueDefault: [0, 0],
      content: '',
      files: []
    }
  },
  methods: {
    showMulLinkageTwoPicker () {
      this.$refs.mpPicker.show()
    },
    onConfirm (e) {
      this.community = e.label
    },
    // onChange (e) {
    // },
    onCancel (e) {
      this.community = ''
    },
    upLoadSuccess (res) {
      this.files = res.files
    },
    sendPublishInfo () {
      let fly = new Fly()
      fly.post('https://mp.miaodongshequ.com/publish', {
        community: this.community,
        title: this.infotitle,
        content: this.content,
        images: this.files
      }).then((res) => {
        console.log(res.data)
      })
        .catch((err) => {
          this.isShowLoading = false
          console.log(err)
        })
    }
  }
}
</script>
<style>
.form {
  margin: 12rpx;
}
.form-group {
  margin: 12rpx 0 12rpx 24rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
textarea,
input {
  border: 1rpx solid #ccc;
}
.mb {
  width: 60%;
  margin: 24rpx 20%;
}
textarea {
  margin-top: 12rpx;
  width: 100%;
}
</style>

