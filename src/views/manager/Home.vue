<template>
  <div class="home">
    <!-- 头部图片 -->
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
   <article>
     
     <!-- 分类6个 -->
     <van-grid :column-num="3">
  <van-grid-item
    v-for="value in categories"
    :key="value.id"
    :icon="value.icon"
    :text="value.name"
  />
</van-grid>
<!-- 产品n个 -->
    <briup-product-item
    @click="toBuyHandler(p)" 
    v-for="p in products" 
    :key="p.id" 
    :data="p">
    </briup-product-item>
   </article>
  </div>
</template>
<script>
import {get,post} from '../../http/axios';
export default {
  data(){
    return{
   categories:[],
   products:[]
    }
  },
  
  created(){
    this.loadCategories();
    this.loadProducts();
  },
  methods:{
    toBuyHandler(p){
      this.$router.push({
      path:"/manager/order_Confirm",
      query:p
      })
    },
    loadCategories(){
    let url="/category/findAll";
    get(url).then((response)=>{
      this.categories = response.data.slice(0,6);
    })
    },
    loadProducts(){
    let url="/product/query";
    let param={
      page:0,
      pageSize:10,
    }
    post(url,param).then((response)=>{
      this.products=response.data.list;
    }
    )

    }

  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>