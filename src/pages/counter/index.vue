<template>
  <div class="weui-article">
    <div class="weui-article__h1">大标题</div>
    <div class="weui-article__section">
      <div class="weui-article__title">章标题</div>
      <div class="weui-article__section">
        <div class="weui-article__h3">1.1 节标题</div>
        <div class="weui-article__p">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
        </div>
        <div class="weui-article__p">
          <image class="weui-article__img"
                 src="@/../static/images/baobiao.png"
                 mode="aspectFit"
                 style="height: 180px" />
          <image class="weui-article__img"
                 src="../../../static/images/bianji.png"
                 mode="aspectFit"
                 style="height: 180px" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// Use Vuex
import store from './store'

export default {
  computed: {
    count () {
      return store.state.count
    }
  },
  methods: {
    increment () {
      store.commit('increment')
    },
    decrement () {
      store.commit('decrement')
    }
  }
}
</script>

<style>
.counter-warp {
  text-align: center;
  margin-top: 100px;
}
.home {
  display: inline-block;
  margin: 100px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
