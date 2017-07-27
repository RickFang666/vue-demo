<template>
  <div id="app">
  <v-header :seller="seller"></v-header>

  <div class="tab">
    <div class="tab-item border-1px">
      <router-link to="/goods" tag="div">商品</router-link>
    </div>
    <div class="tab-item">
      <router-link to="sellers" tag="div">商家</router-link>
    </div>
    <div class="tab-item">
      <router-link to="/ratings" tag="div">评论</router-link>
    </div>
  </div>
  <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
import Header from './components/header/header'
import axios from 'axios'

const ERR_OK = 0

export default {
  name: 'app',
  data() {
    return {
      seller: {}
    }
  },
    components: {
    'v-header': Header
  },
  created() {
    axios.get('api/seller').then((res) => {
      if(res.data.errno === ERR_OK) {
        this.seller = Object.assign({}, this.seller, res.data.data)
      }
      console.log(this.seller)
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"

  #app
    .tab
      display flex
      width 100%
      height 40px
      line-height 40px
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex 1
        text-align center
        & > div
          font-size 14px
          color rgb(77, 85, 93)
        .router-link-active
          color rgb(240, 20, 20)
</style>
