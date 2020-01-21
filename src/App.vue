<template>
  <div id="app">
    <h1>{{title}}</h1>
    <hr/>
    <div>
      <h2>添加商品</h2>
      <div>
        <label for="">商品名称</label>
        <input type="text" v-model="goodsInfo.name">
      </div>
      <div>
        <label for="">商品价格</label>
        <input type="text" v-model="goodsInfo.price">
      </div>
      <div>
        <button @click="addGoodsToList">添加课程到列表</button>
      </div>
    </div>
    <div>
      <h2>商品列表</h2>
      <table>
        <tr>
          <th>商品名称</th>
          <th>商品价格</th>
        </tr>
        <tr v-for="(item,index) in goodsList" :key="item.id">
          <td>{{item.name}}</td>
          <td>{{item.price}}</td>
          <td><button @click="addGoodsToCart(index)">添加到购物车</button></td>
        </tr>
      </table>
    </div>
    <cart :goodsItem="goodsItem" @removeItem="remove"></cart>
  </div>
</template>

<script>
import Cart from './components/Cart'
export default {
  name: 'App',
  components:{
    Cart
  },
   methods: {
      addGoodsToCart(index){
        let item = this.goodsList[index];
        let isHasGoods = this.goodsItem.find(x=>x.id == item.id)
        if(isHasGoods){
          isHasGoods.number += 1;
        }else{
          this.goodsItem.push({
            ...item,
            number: 1,
            isActive: true
          });
        }
      },
      remove(index){
        this.goodsItem.splice(index)
      },
      addGoodsToList(){
        this.goodsList.push(this.goodsInfo)
    }
   },
  data() {
    return{
      title:'购物车',
      //商品信息
      goodsInfo:{
        name:'',
        price: ''
      },
      goodsItem:[

      ],
      goodsList:[
        {
          id: 0,
          name:'Longines浪琴手表',
          price: 10000
        },{
          id: 1,
          name:'迪奥金挚红唇膏999',
          price: 320
        },{
          id: 2,
          name:'CHANEL嘉柏丽尔香水',
          price: 1650
        }
      ]
    }
}
}

</script>
<style scoped>

</style>