<template>
  <div class="remark">
    <textarea placeholder="订单备注(选填)"></textarea>
  </div>
</template>

<script>
    export default {
        name: "remark"
    }
</script>

<style scoped>
  .remark{
    padding: 2rem 0 0;
  }
  .remark textarea{
    width: 100%; height: 5rem; border: 1px solid #ddd; background: #fff; resize: none; padding: 0.6rem; display: block;
  }
</style>
