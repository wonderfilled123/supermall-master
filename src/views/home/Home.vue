<template>
  <div id="home">
    <nav-bar><div slot="center" class="home-nav">购物街</div></nav-bar>
    <scroll class="content"
    ref="scroll"
    :probe-type='3'
    @scroll='contentScroll'
    :pull-up-load='true'
    @pullingUp='loadMore'>
    <home-swiper :banners='banners'>
    </home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行','新款','精选']" class="tab-control" @tabClick="tabClick">
    </tab-control>
    <good-list :goods="showGoods"></good-list>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop">
    </back-top>
  </div>
</template>

<script>
// 自己的组件
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/Featureview'
//  公共的组件
import  NavBar from 'components/common/navbar/NavBar.vue'
import  TabControl from 'components/content/tabControl/TabControl'
import  GoodList  from  'components/content/goods/GoodList'
import Scroll from 'components/common/scroll/Scroll'
import BackTop  from 'components/content/backTop/BackTop'
//  网络模块的组件
import {getHomeMultidata,
        getHomeGoods 
} from 'network/home'



export default {
  components:{
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodList,
    Scroll,
    BackTop
  },
  data(){
    return{
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      },
      currentType:'pop',
      isShowBackTop:false
    }
  },
  computed:{
    showGoods()
    {
      return this.goods[this.currentType].list
    } 
  },
  created(){
    //1.请求多个数据
    this.getHomeMultidata(),

    //2. 请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
    // 3.监听item中图片的加载完成
    this.$bus.$on('itemImageLoad',()=>{
      console.log('----');
      // this.$refs.scroll.scroll.refresh()
    })
  },
  methods:{
    //事件监听方法
    tabClick(index)
    {
      console.log(index);
      switch(index){
        case 0:
         this.currentType='pop'
        break
        case 1:
         this.currentType='new'
        break
        case 2:
         this.currentType='sell'
        break
      }
    },
    backClick()
    {
      this.$refs.scroll.scrollTo(0,0)
      console.log(123);
    },
    contentScroll(position)
    {
      // console.log(position);
      this.isShowBackTop=-(position.y)>1000

    },
    loadMore(){
      console.log('上拉加载更多');
    },
    // 网络请求相关方法
    getHomeMultidata()
    {
    getHomeMultidata().then(res=>{
      // console.log(res);
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend.list;

    })
    },
    getHomeGoods(type)
    {
      const page =this.goods[type].page+1
       getHomeGoods(type,page).then(res=>{
        //  console.log(res);
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page+=1
       })
    }
  }


}
</script>

<style scoped>
   .one
   {
     z-index: 999;
   }
  /* padding-top: 44px; */
  /* height: 100vh; */

.home-nav
{
  background-color: var(--color-tint);
  position:fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.tab-control
{
  position: sticky;
  top: 40px;
  /* background-color: red; */
}
.content{
  height: 300px;
  /* overflow: hidden; */
}

</style>