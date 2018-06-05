<template>
  <header class="header header_fix">
    <a href="javascript:history.back()" class="back_btn"></a>
    在线下单
  </header>
</template>

<script>
    export default {
        name: ""
    }
</script>
<style lang="less" scoped>
  .header{
    position: relative;
    height: 4.8rem;
    line-height: 4.8rem;
    color: #fff;
    font-size: 1.6rem;
    text-align: center;
    background: #ef1a0e;
    width: 100%;
  a{
    position: absolute;
    display: inline-block;
    background: url(http://cdn.xsmore.com/Images/Common/head-back.png) 0 0 no-repeat;
    background-size: 100% 100%;
    width: 2.4rem;
    height: 2.4rem;
    left: 1.2rem;
    top: 1.2rem;
  }
  }
  .header_fix{
    position: fixed;
    top: 0;
    left: 0;
    z-index: 9999;
  }
</style>
