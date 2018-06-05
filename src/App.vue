<template>
  <router-view/>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  html{-ms-text-size-adjust: 100%;-webkit-text-size-adjust: 100%; font-size:10px;}
  body{margin: 0;font-family:'Microsoft YaHei',arial,sans-serif;line-height: 1.5;color: #999; font-size:inherit; background: #f5f5f5;}
  input::-webkit-input-placeholder {line-height: 1.5em;}
  input[type="button"], input[type="submit"], input[type="reset"],input[type="text"],input[type="password"]{-webkit-appearance: listbox;}
  article, aside, details, figcaption, figure, footer, header, hgroup, main, nav, section, summary { display: block;}
  div,ul,ol,li,h1,h2,h3,h4,h5,h6,p,figure,form,blockquote,button{margin: 0;padding:0;}
  button,input,textarea{outline: none;font-family:'Microsoft YaHei','Hiragino Sans GB',STHeiti,arial;}
  a{text-decoration: none; -webkit-tap-highlight-color: transparent; color: #666;}
  li{list-style: none;}
  table{border-collapse: collapse; border-spacing: 0;}
  *{-webkit-box-sizing: border-box; -moz-box-sizing: border-box; box-sizing: border-box;}
  h1,h2,h3{font-weight: normal;}
  h1{font-size: 18px;}
  h2{font-size: 16px;}
  h3{font-size: 14px;}
  b{font-weight: normal;}
  img{border: 0px;max-width: 100%;}
  em{font-style: normal;}
  .clearfix:before,.clearfix:after,.row:before,.row:after{display: table;content:" ";}
  .clearfix:after,.row:after{clear: both;}
  .fff{background: #fff;}
  .fl_l{
    float: left;
  }
  input[type="submit"], input[type="text"],textarea{
    -webkit-appearance: none;
  }
</style>
