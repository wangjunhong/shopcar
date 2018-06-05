<template>
  <div class="order_page">
    <!--头部-->
    <Header></Header>
    <!--地址-->
    <Address></Address>
    <!--备注-->
    <Remark></Remark>
    <!--物品列表-->
    <ul class="com_list">
      <List @showAddCarEvent="showAddCar"></List>
    </ul>
    <!--购物车固定-->
    <div class="shopcar clearfix" @click="shopcarClick">
      <Shopcar :totalPrice="totalPrice" :totalNum="totalNum"></Shopcar>
    </div>
    <!--购物车列表-->
    <GoodsList :class="{active:showGoodsList}" :senGoodLists="getGoodList" @updataInfo="doUpdataInfo"></GoodsList>
    <!--加入购物车-->
    <AddCar :class="{active:AddCarActive}" :status="AddCarActive" :aid="sendAid" @sendInfoToIndex="getInfofromCar"></AddCar>
    <!--背景-->
    <div class="fullbg" @click="hideAll" :class="{active:fullBgActive}"></div>
  </div>
</template>

<script>
  import Header from './common/header'
  import Address from './index/Address'
  import Remark from './index/Remark'
  import List from './index/List'
  import Shopcar from './index/Shopcar'
  import GoodsList from './index/GoodsList'
  import AddCar from './index/AddCar'

    export default {
      name: "index",
      data(){
        return{
          showGoodsList:false,//显示商品列表
          AddCarActive:false,//显示购物车
          fullBgActive:false,//显示全屏
          sendAid:"",
          getGoodList:[],
          totalPrice:0,
          totalNum:0
        }
      },
      components:{
        Header,Address,Remark,List,Shopcar,GoodsList,AddCar
      },
      methods:{
        showAddCar:function (aid) {
          this.AddCarActive=!this.AddCarActive;
          this.fullBgActive=!this.fullBgActive;
          this.sendAid=aid;
        },
        hideAll:function () {
          //点击遮罩隐藏
          this.AddCarActive=false;
          this.showGoodsList=false;
          this.fullBgActive=false;
        },
        shopcarClick:function () {
          //点击
          if(this.totalNum==0){
            this.showGoodsList=false;
            this.fullBgActive=false;
          }else{
            this.showGoodsList=!this.showGoodsList;
            this.fullBgActive=!this.fullBgActive;
          }
        },
        hideShopCar:function () {
          if(this.totalNum==0){
            this.showGoodsList=false;
            this.fullBgActive=false;
          }
        },
        getInfofromCar:function (val) {
          //获取加入购物车的数据 同ID 同类型如果存在++
          this.hideAll();
          for(let i=0;i<this.getGoodList.length;i++){
            if(val.aid==this.getGoodList[i].aid&&val.selIndex==this.getGoodList[i].selIndex){
              this.getGoodList[i].num+=val.num;
              this.countTotal();
              console.log(this.getGoodList);
              return;
            }
          }
          this.getGoodList.push(val);
          this.countTotal();
          console.log(this.getGoodList);
        },
        countTotal:function () {
          if(this.getGoodList.length>0){
            var totalPrice=0;
            var totalNum=0;
            for(let i=0;i<this.getGoodList.length;i++){
              totalPrice+=this.getGoodList[i].price*this.getGoodList[i].num;
              totalNum+=this.getGoodList[i].num;
            }
            this.totalPrice=totalPrice;
            this.totalNum=totalNum;
          }else{
            this.hideAll();
          }
        },
        doUpdataInfo:function (senGoodLists) {
          this.getGoodList=senGoodLists;
          this.countTotal();
          this.hideShopCar();
        }
      }
    }
</script>

<style scoped>
  .fullbg {
    background-color: #000000;
    left: 0;
    opacity: 0.5;
    position: absolute;
    top: 0;
    filter: alpha(opacity=50);
    -moz-opacity: 0.5;
    -khtml-opacity: 0.5;
    display: none;
    width: 100%;
    height: 100%;
    z-index: 9995;
    transition:all 0.3s;
  }
  .fullbg.active{
    display: block;
  }
  .order_page{
    padding: 6rem 0; height: auto;
  }
  .add_shopcar.active{
    bottom: 0;
  }
  .shopcar{
    height: 5rem; width: 100%; background: #fff; position: fixed; bottom: 0; left: 0; border-top: 1px solid #ddd; z-index: 9997;
  }
</style>
