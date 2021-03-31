<template>
<div class="goods">
   <good-list-item :key='item.id' v-for="item in goods" :good-items="item"></good-list-item>
</div>
</template>

<script>

import GoodListItem from './GoodListItem'
export default {
  components:{
    GoodListItem
  },
  props:{
    goods:{
      type:Array,
     default(){
      return []
      }
    }
   
  }
}
</script>

<style>
 .goods
 {
   display: flex;
   flex-wrap: wrap;
   justify-content:space-around;
 }

</style>