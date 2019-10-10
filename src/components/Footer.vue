<template>
  <div class="foot" >
      <div>
         <p> <img src="/static/images/07.png" alt=""></p>
        <p> 商城 </p>
      </div>

       <div>
         <p> <img src="/static/images/08.png" alt=""></p>
        <p> 分类 </p>
      </div>

       <div>
         <p> <img src="/static/images/09.png" alt=""></p>
        <p> 购物车 </p>
      </div>

       <div>
         <p> <img src="/static/images/10.png" alt=""></p>
        <p> 用户中心 </p>
      </div>
  </div>
</template>

<script>
export default {
name:'Footer',

}
</script>

<style>
.foot{
  width: 100%;
  height: 1.6rem;
  font-size: 0.16rem;
  display: flex;
  text-align: center;
}
.foot div{
  width: 25%;
  height: 100%;
}
img{
  margin-top: 0.2rem;
  width: 0.7rem;
  height: 0.65rem;
}
</style>