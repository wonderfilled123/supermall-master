<template>
<div class="goods-item" @click="gooditemclick">
  <img :src="goodItems.show.img" alt="" @load='imageLoad'>
  <div class="goods-info">
    <p>{{goodItems.title}}</p>
      <span class="price">{{goodItems.price}}</span>
      <span class="collect">{{goodItems.cfav}}</span>
  </div>
</div>
</template>

<script>
export default {
  props:{
    goodItems:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods:{
    imageLoad()
    {
      this.$bus.$emit('itemImageLoad')
    },
    gooditemclick()
    {
      this.$router.push('/detail/'+this.goodItems.iid)
    }
  }
}
</script>

<style scoped>
.goods-item
{
  position: relative;
  padding-bottom: 80px;
  width: 48%;
}
.goods-item img
{
  width: 100%;
  border-radius: 5px;
}
.goods-info
{
  font-size: 12px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}
.goods-info p
{
  overflow: hidden;
  text-overflow: ellipsis;
  word-spacing: nowrap;
  margin-bottom:3px;
}
.price 
{
  margin-right: 20px;
  color: var(--color-high-text);
}
.collect
{
  position: relative;
}
</style>