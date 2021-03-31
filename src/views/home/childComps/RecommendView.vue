<template>
<div class="recommend">
  <div v-for=" (item,index) in recommends" class="recommends-item" :key="index" >
    <a :href="item.link">
      <img :src="item.image" alt="">
      <div class="title">
        {{item.title}}
      </div>
    </a>
  </div>
</div>
</template>

<script>
export default {
  props:{
    recommends:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style>
.recommend{
  display: flex;
  width: 100%;
  text-align: center;
  font-style: 12px;
  padding: 10px 0 10px;
  /* padding: 10px 0 10px; */
  border-bottom: 8px solid #eee;
}
.recommends-item
{
  flex: 1;
}
.recommends-item img
{
  width: 70px;
  height: 70px;
}

</style>