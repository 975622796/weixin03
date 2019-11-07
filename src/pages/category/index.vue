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
    this.getCategories()
  },
  methods: {
    getCategories () {
     this.$request () ({
        url:'/api/public/v1/categories'
     }).then(data=>{
        console.log(data)
        this.categories=data
     })
    }
  },
}
</script>

<style>
</style>