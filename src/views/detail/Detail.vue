<template>
  <div>
    <detail-nav-bar>
    </detail-nav-bar>
    <detail-bottom-bar class="bottombar" @addCart='addToCart' @click='add'>
    </detail-bottom-bar>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import {getDetail} from 'network/detail'
import DetailBottomBar from './childComps/DetailBottomBar'
export default {
  components:{
    DetailNavBar,
    DetailBottomBar
  },
  data()
  {
    return{
      iid:null
    }
  },
  created()
  {
    //1.保存传入的id
    this.iid=this.$route.params.iid
    //2.根据iid请求详情数据
    getDetail(this.iid).then(res=>{
      console.log(res);
    })

  },
  methods:{
    addToCart()
    {
      console.log('-----');
    },
  }
}
</script>

<style>
.bottombar
{
  position: relative;
  top: 400px;
}
</style>