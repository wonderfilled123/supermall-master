<template>
<div class="wrapper" ref="wrapper">
  <div class="content">
    <slot></slot>
  </div>
</div>
</template>

<script>

import BScroll, { ObserveDom } from 'better-scroll'
export default {
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type:Boolean,
      default:false
    }
  },
  data(){
    return{
      scroll:null
    }
  },
  mounted(){
    //1. 创建 BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper,{
      observeDOM:true,
      mouseWheel:true,
      click:true,
      probeType:this.probeType,
      pullUpLoad:this.pullUpLoad
    })
    // this.scroll.scrollTo(0,0)
    // 2. 监听滚动位置
    this.scroll.on('scroll',(position)=>{
      // console.log(position);
      this.$emit('scroll',position)
    })
    //3. 监听上拉加载事件
    this.scroll.on('pullingUp',()=>{
      this.$emit('pullingUp')
    })
  },
  methods: {
    scrollTo(x,y,time=300){
      this.scroll.scrollTo(x,y,time)
    }
  }
}
</script>

<style>
   /* height: 1000px; */
 
</style>