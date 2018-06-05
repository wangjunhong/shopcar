<template>
    <div class="submit_wrap">
      <a href="javascript:" class="car">
        <i></i>
        <em>{{totalNum}}</em>
      </a>
      产品金额：<span>￥<em>{{totalPrice}}</em></span>
      <a href="javascript:" class="submit_btn" @click="stopDefault">提交订单</a>
    </div>
</template>

<script>
    export default {
      name: "shopcar",
      props:['totalPrice','totalNum'],
      methods:{
        stopDefault:function (e) {
          e.stopPropagation()
        }
      }
    }
</script>

<style scoped>

  .submit_wrap{
    padding: 1rem; height: 100%; line-height: 3rem; font-size: 1.4rem; color: #333;
  }
  .car{
    position: relative; width: 3rem; height: 3rem; padding: 0.5rem; background:#f5f5f5; display: block; float: left; margin-right: .5rem;
  }
  .car i{
    width: 2rem; height: 2rem; background: url(../../assets/images/icons/car.png) no-repeat; background-size: 100%; background-position: center; display: block;
  }
  .car em{
    background: #72a52c; color: #fff; border-radius: 50%; position: absolute; width: 1.6rem; height: 1.6rem; line-height: 1.6rem; right: -0.5rem; top: -0.5rem; text-align: center;
  }
  .submit_wrap .submit_btn{
    position: absolute; right: 0; top: -0.1rem; height: 5rem; line-height: 5rem; font-size: 1.6rem; width: 8rem; text-align: center; background: #72a52c; color: #fff;
  }
  .submit_wrap span{
    color: #72a52c; font-weight: 700;
  }
  .sjx{
    width: 0;
    height: 0;
    border-left: .5rem solid transparent;
    border-right: .5rem solid transparent;
    border-top: 0.8rem solid #fff;
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
</style>
