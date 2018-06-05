<template>
  <div class="add_shopcar">
    <div class="rel">
      <div class="product_info">
        <img :src="getInfo.img" alt="">
        <h2>{{getInfo.goodsName}}</h2>
        <span>请选择</span>
      </div>
      <!-- 包装 -->
      <div class="div_rel packing">
        <span class="title_span">包装：</span>
        <div class="clearfix">
          <a href="javascript:" @click="selSpecifications(index)" :class="{active:index==selIndex}" v-for="(item,index) in getInfo.specifications" :key="index">{{item|toGenderText}}</a>
        </div>
      </div>
      <div class="div_rel specifications">
        <span class="title_span">价格：</span>
        <div class="clearfix">
          <a href="javascript:" class="active">￥{{price}}</a>
        </div>
      </div>
      <div class="div_rel total">
        <span class="title_span">合计：</span>
        <div class="clearfix">
          <span class="money">￥<em>{{price*number}}</em></span>
          <div class="add_reduce">
            <a href="javascript:" @click="reduceNum" class="reduce_btn"></a>
            <input type="number" oninput="if(value.length>3)value=value.slice(0,3)"  v-model="number" name="" class="sel_num_input">
            <a href="javascript:" @click="addNum" class="add_btn"></a>
          </div>
        </div>
      </div>
      <div class="add_to_shopcar">
        <a id="addcar_btn" @click="addShopCar" href="javascript:">加入购物车</a>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
      name: "add-car",
      props:['status','aid'],
      data(){
        return{
          goodsInfo:{
            goodDetail:[
              {
                aid:"0101",
                img:"//img.alicdn.com/bao/uploaded/i3/3171302631/TB24oDgugRkpuFjy1zeXXc.6FXa_!!3171302631.jpg_240x240.jpg",
                goodsName:"寒透国",
                specifications:[0,1],
                price:[3,15],
              },{
                aid:"0102",
                img:"//img.alicdn.com/bao/uploaded/i1/3171302631/TB2EqLvjNOMSKJjSZFlXXXqQFXa_!!3171302631.jpg_240x240.jpg",
                goodsName:"包心耙",
                specifications:[1,2],
                price:[2,10],
              },{
                aid:"0103",
                img:"//img.alicdn.com/bao/uploaded/i3/3171302631/TB2Q9I4nLDH8KJjy1XcXXcpdXXa_!!3171302631.jpg_240x240.jpg",
                goodsName:"山芋",
                specifications:[0,1,2],
                price:[3,5,15],
              },{
                aid:"0104",
                img:"//img.alicdn.com/bao/uploaded/i2/3171302631/TB23ce.mm3PL1JjSZFxXXcBBVXa_!!3171302631.jpg_240x240.jpg",
                goodsName:"芝麻",
                specifications:[2],
                price:[50],
              }
            ]
          },
          getInfo:{

          },
          selIndex:0,
          number:1,//数量
          price:0,//单价
          totalPrice:0//总价
        }
      },
      filters:{
        toGenderText:function (val) {
          var textArr=['袋','个','斤'];
          return textArr[val];
        }
      },
      watch:{
        status:function () {
          this.selIndex=0;
          this.number=1;
          if(this.status){
            var list = this.goodsInfo.goodDetail;
            for(let i of list){
              if(i.aid==this.aid){
                this.getInfo=i;
                this.price=this.getInfo.price[this.selIndex];
                return;
              }
            }
          }
        }
      },
      methods:{
        selSpecifications:function (val) {
          this.selIndex=val;
          this.price=this.getInfo.price[val];
        },
        reduceNum:function () {
          this.number=Math.max(1,--this.number);
        },
        addNum:function () {
          this.number=Math.min(99,++this.number);
        },
        addShopCar:function () {
          var obj={
            aid:this.aid,
            num:parseInt(this.number),
            price:this.price,
            selIndex:this.selIndex,
            goodsName:this.getInfo.goodsName,
            img:this.getInfo.img
          };
          this.$emit('sendInfoToIndex',obj);
        }
      }
    }
</script>

<style scoped>
  .add_shopcar{
    position: fixed; bottom: -50rem; left: 0; z-index: 9997; background: #fff; width: 100%; transition:all 0.3s;
  }

  .add_shopcar .product_info{
    position: relative; padding-left: 8rem; height: 6rem;
  }
  .add_shopcar .product_info h2{
    font-size: 1.4rem; color: #333; font-weight: 700; margin-top: 0.5rem;
  }
  .add_shopcar .product_info span{
    font-size: 1.2rem; color: #777977;
  }
  .add_shopcar .product_info img{
    width: 6rem; position: absolute; left: 1rem;top: -1rem;
  }

  .add_shopcar .div_rel{
    position: relative; padding-left: 4rem;
  }
  .add_shopcar .div_rel .title_span{
    position: absolute; font-size: 1.2rem; color: #333; left: 1rem; top: 0;
  }
  .packing{
    height: 4rem; line-height: 4rem;
  }
  .packing a{
    padding: 0 1rem; height: 2rem; margin: 1rem 1rem 0 0; line-height: 2rem; text-align: center; display: block; float: left; color: #333;  border-radius: 0.4rem; border: 1px solid #ddd;
  }
  .packing a.active{
    color: #fff; background: #72a52c; border-color: #72a52c;
  }
  .specifications{
    height: 3rem; line-height: 3rem; background: #f5f5f5; border-top: 1px solid #ddd;
  }
  .specifications a{
    padding: 0 1rem; height: 2rem; color: #333; border: 1px solid #ddd; display: block; float: left; line-height: 2rem; text-align: center; margin: .5rem 1rem 0 0 ;
  }
  .specifications a.active{
    border-color: #72a52c; color: #72a52c;
  }
  .total{
    height: 4rem; line-height: 4rem; padding: 0 1rem 1rem 4rem;
  }
  .add_reduce{
    font-size: 0; position: relative; float: right; line-height: 0; top: 1rem;
  }
  .sel_num{
    display: inline-block;
    margin-left: 1.0rem;
    width: auto;
  }
  .sel_num_input {
    width: 7.8rem; height: 2.4rem; border: .1rem solid #ddd; font-size: 1.4rem; color: #777977; text-align: center;
  }
  .sel_num .sel_num_input:focus{
    border-color: #ddd;
  }
  .add_reduce a{
    width: 2.4rem; height: 2.4rem; transition: unset; display: inline-block; position: absolute; top: 0; left: 0; border: .1rem solid #ddd;
    background: url(../../assets/images/icons/reduce.png) no-repeat;   background-size: 60%; background-position: center;
  }
  .add_reduce .add_btn{
    left: 5.4rem;  background: url(../../assets/images/icons/add.png) no-repeat;  background-size: 60%;  background-position: center;
  }
  .add_to_shopcar {
    padding: 0.2rem;
  }
  .add_to_shopcar a{
    display: block; width: 100%; height: 4rem; line-height: 4rem; background: #72a52c; text-align: center; font-size: 1.6rem; color: #fff;
  }
  .money{
    color: #72a52c; font-weight: 700; font-size: 1.4rem;
  }
  .money em{
    font-size: 1.6rem;
  }

  .add_shopcar{
    position: fixed; bottom: -50rem; left: 0; z-index: 9997; background: #fff; width: 100%; transition:all 0.3s;
  }

  .sel_num_input{
    -webkit-user-select: auto;
    -moz-user-select: auto;
    -ms-user-select: auto;
    user-select: auto;
  }
</style>
