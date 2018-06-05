<template>
    <div>
      <div class="order_address">
        <i></i>
        <h2>{{name}}<span>{{phone}}</span></h2>
        <p>{{address}}</p>
      </div>
    </div>
</template>

<script>
    export default {
        name: "",
      data(){
          return{
            name:"小明",
            phone:"17899998888",
            address:"浙江省杭州市西湖区西湖文化广场1栋"
          }
      }
    }
</script>

<style scoped>

  .order_address{
    background: #fff; padding: 1rem 1rem 1rem 4rem; position: relative;
  }
  .order_address i{
    width: 2rem; height: 2rem; background: url(../../assets/images/icons/address.png) no-repeat; background-size: 100%; position: absolute; left: 1rem; top: 2rem;
  }
  .order_address h2{
    font-size: 1.6rem; color: #333; font-weight: 700;
  }
  .order_address h2 span{
    float: right; font-size: 1.4rem;
  }
  .order_address p{
    font-size: 1.4rem; color: #666;
  }
</style>
