<template>
    <div>
        <h2>我是购物车</h2>
        <table>
            <tr>
                <td>勾选</td>
                <td>商品名称</td>
                <td>商品价格</td>
                <td>数量</td>
                <td>价格</td>
            </tr>
            <tr v-for="(item,index) in goodsItem" :key="item.id">
                <td>
                    <input type="checkbox" v-model="item.isActive">
                </td>
                <td>{{item.name}}</td>
                <td>{{item.price}}</td>
                <td>
                    <button @click="minus(index)">-</button>
                    {{item.number}}
                    <button @click="add(index)">+</button>
                </td>
                <td>{{item.price*item.number}}</td>
            </tr>
            <tr>
                <td></td>
                <td colspan="2">{{isActiveGoods}}/{{allGoodsList}}</td>
                <td colspan="2">{{allPrice}}</td>
            </tr>
        </table>
    </div>
</template>
<script>
    export default{
        // 遵守单项数据流
        props:['goodsItem'],
        methods:{
            minus(index){
                let number = this.goodsItem[index].number;
                if(number > 1){
                    this.goodsItem[index].number -=1;
                }else{
                    if(window.confirm('确定要出删除吗')){
                        this.$emit('removeItem',index)
                    }
                }
            },
            add(index){
                this.goodsItem[index].number +=1;
            }
        },
        computed:{
            isActiveGoods(){
                return this.goodsItem.filter(item => item.isActive).length
            },
            allGoodsList(){
                return this.goodsItem.length
            },
            allPrice(){
                let num = 0;
                this.goodsItem.forEach(item=>{
                    if(item.isActive){
                        num+= item.price * item.number
                    }
                })
                return num;
            }
        }
    }
</script>
<style scoped>

</style>