<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <a v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header/header'
const ERR_OK = 0;

export default{
  data(){
      return{
          seller:{}
      }
  },
  created(){
      this.$http.get('/api/seller').then((response) => {
          response = response.body;
          if (response.errno === ERR_OK){
              this.seller = response.data;
              console.log(this.seller)

          }
      });
  },
  components: {
    'v-header':header
  }
}
</script>

<style lang="less" rel="stylesheet/less">
  .tab{
    display:flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    .tab-item{
      flex: 1;
      text-align: center;
    }
    &>a{
      display: block;
      text-decoration: none;
      font-size: 14px;
      color: rgb(77,85,93);
    }
    .active{
    color: rgb(240,20,20);
    }
  }
</style>
