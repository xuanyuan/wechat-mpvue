<template>
  <div>办证</div>
</template>
<script>
export default {
  data () {
    return {

    }
  },
  // 路由传参
  onShow () {
    const query = this.$root.$mp.query
    this.getInfoListByType(query.type)
  },
  methods: {
    getInfoListByType (type) {

    }
  }
}
</script>
<style>
</style>

