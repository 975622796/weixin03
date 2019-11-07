<template>
  <div class="wrapper">
    <search @confirm="toSearchList"
            @input="inputHandler"
            :keyword="keyword" />
    <div class="history-search">
      <div class="title">
        <span class="title">历史搜索</span>
        <icon type="clear"
              size="18"
              @click="clearKeywordList">
        </icon>
      </div>
      <ul>
        <li v-for="(item, index) in keywordList"
            :key="index"
            @click="clickSearch(item,index)">{{item}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Search from '@/components/search.vue'
export default {
  data () {
    return {
      keyword: '',
      keywordList: wx.getStorageSync('keyword_list') || []
    }
  },
  components: {
    Search
  },
  onShow () {
    this.keywordList = wx.getStorageSync('keyword_list') || []
  },
  methods: {
    inputHandler (params) {
      this.keyword = params
    },
    clickSearch (item, index) {
      let _keywordList = [...this.keywordList]
      _keywordList.splice(index, 1)
      _keywordList.unshift(item)
      wx.setStorageSync('keyword_list', _keywordList)

      wx.navigateTo({ url: `/pages/list/main?keyword=${item}` })
      this.keyword = ''
    },
    toSearchList () {
      if (!this.keyword) {
        return
      }

      // 去重放前面
      let _keywordList = [...this.keywordList]
      if (!_keywordList.includes(this.keyword)) {
        _keywordList.unshift(this.keyword)
      }
      wx.setStorageSync('keyword_list', _keywordList)

      wx.navigateTo({ url: `/pages/list/main?keyword=${this.keyword}` })
      this.keyword = ''
    },
    clearKeywordList () {
      wx.showModal({
        title: '提示',
        content: '你确定要删除吗',
        showCancel: true, // 是否显示取消按钮,
        cancelText: '取消', // 取消按钮的文字，默认为取消，最多 4 个字符,
        cancelColor: '#000000', // 取消按钮的文字颜色,
        confirmText: '确定', // 确定按钮的文字，默认为取消，最多 4 个字符,
        confirmColor: '#3CC51F', // 确定按钮的文字颜色,
        success: res => {
          if (res.confirm) {
            this.keywordList = []
            wx.setStorageSync('keyword_list', [])
          }
        }
      })
    }
  }
}
</script>

<style lang="less">
.search {
  background-color: #eee;
  padding: 30rpx 15rpx;
  display: flex;
  justify-content: space-between;
  font-size: 28rpx;
  position: relative;
  icon {
    position: absolute;
    top: 50rpx;
    left: 38rpx;
  }
  input {
    height: 60rpx;
    flex: 1;
    background-color: #fff;
    padding-left: 70rpx;
    box-sizing: border-box;
    border-radius: 4rpx;
  }
  button {
    width: 160rpx;
    height: 60rpx;
    line-height: 60rpx;
    border-radius: 8rpx;
    font-size: 28rpx;
    border: 1rpx solid #bfbfbf;
    background-color: #eee;
    margin-left: 20rpx;
  }
}

.history-search {
  color: #333;
  font-size: 28rpx;
  padding: 30rpx 30rpx 30rpx 15rpx;
  .title {
    display: flex;
    justify-content: space-between;
  }

  ul {
    display: flex;
    flex-wrap: wrap;
    margin-top: 30rpx;
    li {
      height: 64rpx;
      line-height: 64rpx;
      padding: 0 26rpx;
      background-color: #ddd;
      margin: 0 30rpx 16rpx 0;
    }
  }
}
</style>