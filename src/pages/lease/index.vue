<template>
  <div>
    <mp-searchbar :value="inputValue"
                  :placeholder="搜索"
                  confirmType="search"
                  @confirm="confirm">
    </mp-searchbar>
    <div class="weui-cells weui-cells_after-title">
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
  </div>
</template>
<script>
import mpSearchbar from 'mpvue-weui/src/searchbar'
export default {
  data () {
    return {

    }
  },
  components: {
    mpSearchbar
  }
}
</script>
<style>
.single-line {
  display: inline-block;
  vertical-align: middle;
}
</style>

