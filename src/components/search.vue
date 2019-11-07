<template>
  <div class="header">
    <input type="text"
           :value="inputVal"
           @input="handleInput"
           @confirm="$emit('confirm')">
    <icon class="search-icon"
          type="search"
          size="16">
    </icon>
    <icon class="clear-icon"
          type="clear"
          size="16"
          color="#ccc"
          v-show="inputVal"
          @click="inputVal=''">
    </icon>
  </div>
</template>

<script>
export default {
  props: ['keyword'],
  data () {
    return {
      inputVal: this.keyword
    }
  },
  methods: {
    handleInput (event) {
      this.inputVal = event.target.value
      this.$emit('input', this.inputVal)
    }
  },
  watch: {
    keyword (value) {
      this.inputVal = value
    }
  }
}
</script>

<style lang="less" scoped>
.header {
  height: 120rpx;
  background-color: #eee;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  input {
    background-color: #fff;
    height: 60rpx;
    width: 720rpx;
    padding-left: 74rpx;
    box-sizing: border-box;
  }
  .search-icon {
    position: absolute;
    left: 44rpx;
  }

  .clear-icon {
    position: absolute;
    right: 44rpx;
    z-index: 100;
  }
}
</style>