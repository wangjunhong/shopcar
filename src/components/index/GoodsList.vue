<template>
  <div class="goods_list">
    <div class="rel">
      <h2>购物车<a class="clear_btn" @click="clearAll"><i></i>清空</a></h2>
      <ul class="pro_list">
        <li v-for="(item,index) in senGoodLists" v-if="item.num>0" :key="index">
          <img :src="item.img" alt="">
          <div class="fl_l">
            <h2>{{item.goodsName}}</h2>
            <p>
              <span>包装：{{item.selIndex|toGenderText}}</span> <br>
              <span>单价：<em>￥{{item.price}}</em></span>
            </p>
          </div>
          <div class="add_reduce_radio">
            <a href="javascript:" @click="reduceNum(index)" class="reduce_btn"></a>
            <input type="number" v-model="inputItemNum=item.num" @keyup="inputNum(index)" readonly class="sel_num_input">
            <a href="javascript:" @click="addNum(index)" class="add_btn"></a>
          </div>
        </li>
      </ul>
      <i class="sjx"></i>
    </div>
  </div>
</template>

<script>
    export default {
      name: "goods-list",
      props:['senGoodLists'],
      filters:{
        toGenderText:function (val) {
          var textArr=['袋','个','斤'];
          return textArr[val];
        }
      },
      data(){
        return{
          inputItemNum:null
        }
      },
      methods:{
        reduceNum:function (index) {
          this.senGoodLists[index].num=Math.max(0,--this.senGoodLists[index].num);
          this.$emit('updataInfo',this.senGoodLists);
        },
        addNum:function (index) {
          this.senGoodLists[index].num=Math.min(99,++this.senGoodLists[index].num);
          this.$emit('updataInfo',this.senGoodLists);
        },
        inputNum:function (index) {
          this.inputItemNum=this.senGoodLists[index].num;
          this.$emit('updataInfo',this.senGoodLists);
        },
        clearAll:function () {
          let self=this;
          self.$layer.confirm("确定要删除吗？",function(){
             for(let i=0;i<self.senGoodLists.length;i++){
              self.senGoodLists[i].num=0;
            }
            self.$emit('updataInfo',self.senGoodLists);
            self.$layer.closeAll();
          });
        }
      }
    }
</script>

<style scoped>
  .add_shopcar.active{
    bottom: 0;
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
  .sjx{
    width: 0;
    height: 0;
    border-left: .5rem solid transparent;
    border-right: .5rem solid transparent;
    border-top: 0.8rem solid #fff;
  }
  .goods_list .sjx{
    position: absolute; bottom: -0.8rem ;left: 2rem;
  }
  .goods_list{
    position: fixed; bottom: -40rem; left: 0; width: 100%; background: #fff; z-index: 9998; transition: all 0.3s;
  }
  .goods_list.active{
    bottom: 7rem;
  }
  .goods_list .rel > h2{
    padding: 1rem; font-size: 1.6rem; color: #333; font-weight: 700; background: #f5f5f5;
  }
  .goods_list h2 a{
    float: right; color: #666; font-size: 1.4rem; font-weight: normal;
  }
  .goods_list h2 a i{
    width: 1.6rem; height: 1.6rem; display: block; position: relative; top: 0.2rem; float: left; background: url(../../assets/images/icons/remove.png) no-repeat; background-size: 100%;
  }
  .goods_list .pro_list{
    max-height: 34rem; overflow: auto;
  }
  .goods_list .pro_list li{
    padding: 0.5rem 1rem 0.5rem 6rem; height: 6rem;
  }
  .goods_list .pro_list li img{
    top: 1rem; border: 1px solid #ddd; padding: 0.2rem;
  }
  .goods_list .pro_list li h2{
    margin-bottom: 0;
    width: 15rem;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .specifications_span{
    display: block;
  }
  .add_reduce_radio{
    float: right; padding-top: 1.6rem;
  }
  .add_reduce_radio a{
    width: 1.6rem; height: 1.6rem; display: block; float: left; background: url(../../assets/images/icons/reduce_o.png) no-repeat; background-size: 100%;
  }
  .add_reduce_radio .add_btn{
    background: url(../../assets/images/icons/add_o.png)  no-repeat; background-size: 100%;
  }
  .goods_list .sel_num_input{
    width: 3rem; float: left; height: 1.6rem; margin: 0 0.2rem; font-size: 1.2rem;
  }

  .sel_num_input{
    -webkit-user-select: auto;
    -moz-user-select: auto;
    -ms-user-select: auto;
    user-select: auto;
  }

  .vl-notify{
    z-index: 9999;
  }
</style>
