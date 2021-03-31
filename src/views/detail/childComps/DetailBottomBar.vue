<template>
<div class="bottom-bar">
   <div class="info">
     详情
   </div>
   <div class="shopcar" @click='addToCart'>
     加入购物车
   </div>
   <div class="buy">
     购买
   </div>
</div>
</template>

<script>
export default {
  data(){
    return {

    }
  },
  methods:{
    addToCart()
    {
      // console.log('点击添加到购物车');
      // 我在子组件里监听的是组件内部的东西，我在父组件使用子组件时候监听的是整个组件
      this.$emit('addCart')
    }
  }

}
</script>

<style>
.bottom-bar
{
  height: 49px;
  display: flex;
  text-align: center;
  color: black;
  line-height: 49px;
  font-size: 15px;
  /* position: relative; */
  /* margin-top: 0; */
  /* background-color: red; */
}
.info
{
  flex: 2;
  background-color:#2980b9;
}
.shopcar
{
  flex: 1;
  background-color:#e74c3c;

}
.buy
{
  flex:1;
  background-color: #d35400;
}
</style>