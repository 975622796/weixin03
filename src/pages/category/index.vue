<template>
  <div>
    <!-- 头部搜索 -->
    <SearchHotspot />
    <div class="main">

      <div class="left">

      </div>
    </div>
  </div>

</template>

<script>
import SearchHotspot from '@/components/searchhotspot'
export default {
  data () {
    return {
      activeIndex: 0,
      // 分类数据
      categories: [],
      isInit: false
    }
  },
  components: {
    SearchHotspot
  },
  onLoad () {
     this.get
  }
}
</script>

<style>
</style>