<template>
  <div id="app">
   <v_header :seller='seller'></v_header>
    <div class="tab">
      <div class="item-tab">
         <router-link to="/goods" class="item_link">商品</router-link>
      </div>
      <div class="item-tab">
        <router-link to="/ratings" class="item_link">评价</router-link>
      </div>
      <div class="item-tab">
        <router-link to="/seller" class="item_link">商家</router-link>
      </div>
    </div>
   <router-view :seller="seller"></router-view>
  
  </div>
</template>

<script>
import v_header from "./components/header/header"
import axios from 'axios'


export default {
  data(){
    return {
      seller:{}
    }
  },
  created:function(){
     this.$nextTick(function () {
      this.$http.get('/api/seller').then((responed) =>{
      responed = responed.body
      
      this.seller = responed.data

      console.log(this.seller)
    })
  })
   

  },
    
  components:{
    v_header
  }
}

</script>

<style type="text/css">

 #app .tab{
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  border-bottom: 1px solid rgba(7,17,27,0.1)
 }
 #app .tab .item-tab{
  flex: 1;
  text-align:center;
 }

 .item_link{
  display: block;
  text-decoration: none;
  font-size: 14px;
  color: rgb(77,85,93);
 }
 .router-link-active{
  color: rgb(240,20,20);
 }
</style>

