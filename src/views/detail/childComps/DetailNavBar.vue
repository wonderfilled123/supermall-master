<template>
  <div class="detail">
    <nav-bar>
      <div slot="left" class="back" @click="backclick">
        <img src="~assets/images/common/back.svg" alt="">
      </div>
    <div slot="center" class="title">
      <div v-for="(item,index) in titles"
      :key="item"
      class="title-item"
      @click="itemclick(index)"
      :class="{active:index===currentIndex}" >{{item}}</div>
    </div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
export default {
  components:{
    NavBar
  },
  data(){
    return{
      titles:['商品','参数','评论','对象'],
      isactive:true,
      currentIndex:0
    }
  },
  created()
  {
    
  },
  methods:{
    itemclick(index)
    {
      this.currentIndex=index
    },
    backclick()
    {
      this.$router.back()
    }
  }
}
</script>

<style scoped>
/* .center span
{
  padding:2px 5px;
}, */
.title
{
 display: flex;
}
.title-item
{
  flex: 1;
  font-size: 13px;
}
.active
{
  color: red;
}
.back img
{
  margin-top: 10px;
}

</style>