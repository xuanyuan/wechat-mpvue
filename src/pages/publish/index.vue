<template>
  <div class="publish-box">
    <div class="community-box">
      <input type="text"
             disabled
             width="70%"
             v-model="community" />
      <mp-button type="default"
                 size="small"
                 @click="showMulLinkageTwoPicker">选择小区</mp-button>
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
    <input type="text"
           maxlength="20"
           placeholder="输入标题" />
    <textarea name="发布信息"
              id=""
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
        },
        {
          label: '火车票',
          value: 200,
          children: [
            {
              label: '卧铺',
              value: 210
            },
            {
              label: '坐票',
              value: 202
            },
            {
              label: '站票',
              value: 203
            }
          ]
        },
        {
          label: '汽车票',
          value: 300,
          children: [
            {
              label: '快班',
              value: 301
            },
            {
              label: '普通',
              value: 302
            }
          ]
        }
      ],
      community: '',
      pickerValueDefault: [1, 0]
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
      console.log(res)
    }
  }
}
</script>
<style>
mp-button {
  display: flex;
  justify-content: center;
}
.publish-box {
  margin: 12rpx;
}
.community-box {
  margin: 12rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
textarea,
input {
  border-radius: 5px;
  border: 1rpx solid #ccc;
}
community-box input {
  width: calc(100% - 160rpx);
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

