<template>
    <li>
      <h2>{{titleName}}</h2>
      <ul class="pro_list">
        <li v-for="(item,index) in goodsList" :key="index">
          <img :src="item.img" alt="">
          <h2>{{item.goodsName}}</h2>
          <span>规则：{{item.specifications|toGenderText}}</span>
          <a href="javascript:" class="order_btn" :data-aid="item.aid"  @click="showAddCar(item.aid)">在线下单</a>
        </li>
      </ul>
    </li>
</template>

<script>
    export default {
      name: "list",
      data(){
          return{
            titleName:"望江小商品",
            goodsList:[{
              img:"//img.alicdn.com/bao/uploaded/i3/3171302631/TB24oDgugRkpuFjy1zeXXc.6FXa_!!3171302631.jpg_240x240.jpg",
              specifications:"0",
              goodsName:"寒透国",
              aid:"0101"
            },{
              img:"//img.alicdn.com/bao/uploaded/i1/3171302631/TB2EqLvjNOMSKJjSZFlXXXqQFXa_!!3171302631.jpg_240x240.jpg",
              specifications:"1",
              goodsName:"包心耙",
              aid:"0102"
            },{
              img:"//img.alicdn.com/bao/uploaded/i3/3171302631/TB2Q9I4nLDH8KJjy1XcXXcpdXXa_!!3171302631.jpg_240x240.jpg",
              specifications:"2",
              goodsName:"山芋",
              aid:"0103"
            },{
              img:"//img.alicdn.com/bao/uploaded/i2/3171302631/TB23ce.mm3PL1JjSZFxXXcBBVXa_!!3171302631.jpg_240x240.jpg",
              specifications:"2",
              goodsName:"芝麻",
              aid:"0104"
            }]
          }
      },
      methods:{
        showAddCar:function (aid) {
          this.$emit('showAddCarEvent',aid);
        }
      },
      filters:{
        toGenderText:function (val) {
          var textArr=['袋','个','斤'];
          return textArr[val];
        }
      }
    }
</script>

<style>
  .com_list li{
    background: #fff; margin-top: 1rem; font-size: 1.3rem;
  }
  .pro_list li:first-child{
    margin-top: 0;
  }
  .com_list >li >h2{
    height: 4rem; line-height: 4rem; font-weight: 700; font-size: 1.6rem; color: #333; padding-left: 1rem;
  }
  .pro_list li{
    height: 8rem; border-top: 1px solid #ddd; position: relative; padding: 2rem 2rem 2rem 6rem;
  }
  .pro_list li h2{
    font-size: 1.4rem; color: #333; font-weight: 700; margin-bottom: 1rem;
  }
  .pro_list li img{
    position: absolute; left: 1rem; top: 2rem; width: 4rem;
  }
  .order_btn{
    position: absolute; top: 3rem; right: 2rem; width: 6rem; height: 2rem; line-height: 2rem; background: #72a52c; border-radius: 0.8rem; display: block; color: #fff; text-align: center;
  }
</style>
