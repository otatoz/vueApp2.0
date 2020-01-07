<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
    <van-grid :column-num="3">
      <van-grid-item
        v-for="item in categories"
        :key="item.id"
        :icon="item.icon"
        :text="item.name"
      />
    </van-grid>

    <!-- <van-grid :column-num="3">
      <van-grid-item
        v-for="item in products"
        :key="item.id"
        :icon="item.photo"
        :text="item.name"
      />
    </van-grid> -->
    <briup-product-item v-for="item in products" :key="item.id" :data='item' @click="toOrderHandler(item)">
      
    </briup-product-item>
  </div>
</template>
<script>
import {mapState, mapActions} from 'vuex'
import {get,post} from '../../http/axios'
export default {
  data(){
    return {
      categories:[],
      products:[]
    }
  },
  created(){
    this.loadCategory()
    this.loadProduct()
  },
  methods:{
    toOrderHandler(item){
      this.$router.push({
        path:'order_conform',
        query:item
      })
    },
    loadCategory(){
      get('/category/findAll').then((res)=>{
        this.categories = res.data.slice(0,6)
      })
    },
    loadProduct(){
      let params = {
        page:0,
        pageSize:3
      }
      post('/product/query',params).then((res)=>{
        this.products = res.data.list
      })
      
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