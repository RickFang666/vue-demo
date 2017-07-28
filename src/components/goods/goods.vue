<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper"></div>
  </div>
</template>

<script type="text/ecmascript-6">

import axios from 'axios'

const ERR_OK = 0

export default {
  data() {
    return {
      goods: []
    }
  },
  created() {
    axios.get('api/goods').then((res) => {
      if(res.data.errno === ERR_OK){
        this.goods = res.data.data
      }
      console.log(this.goods)
    })
    this.classMap = ['decrease','discount','guarantee','invoice','special']
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .goods
    position absolute
    display flex
    top 174px
    bottom 46px
    width 100%
    overflow hidden
    .menu-wrapper
      flex 0 0 80px
      width 80px
      background #f3f5f7
      .menu-item
        display table

    .foods-wrapper
      flex 1

</style>
