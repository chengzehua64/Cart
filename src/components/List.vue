<template>
  <div class="qw" >
      <div class="pin" >
        <p></p>
         <p>平台自营</p> 
      </div> 
      <div class="nei"  v-for="(item,key) in list" :key='key' >
       <div class="checked" > <input type="checkbox" v-model='item.done' @change="onchange(key)" ></div>
       <div class="img" > <img :src="'/static/images/'+item.img" alt=""> </div>
         <div class="yi" >
           <p class="w" > {{item.name}}</p> 
           <p class="q" > 颜色:蓝色8010 </p>
           <p class="q" > 适合身高:73cm (适合5-10月) </p>
           <p  > <span class="e" > ￥{{item.price}} </span>
             <span class="r" > 
               <button @click="jian(key)" >-</button>
              {{item.num}}
              <button @click="jia(key)">+</button>
              </span>
            </p>
          </div>
      </div>
      <div class="quan" >
          <p> <input type="checkbox" @click="xuan()" v-model="flag" > 全选 </p>
          <p> <span> 总计:￥{{ji}}</span></p>
          <p class="bian" v-if="!bian" @click="bianji()" ><button  >编辑</button></p>
          <p class="bian" v-else @click="bian=!bian" ><button  >完成</button></p>
          <p class="jie" v-if="!bian" ><button>结算</button></p>
          <p class="jie" v-if="bian" @click="shan()" ><button>删除</button></p>
      </div>

    <div class="bie" v-if="tan" >
      <div class="kuang"  v-if="tan"   >
        <p>提示</p>
           <p>确认删除 {{asd}}项内容吗？</p> 
       <p class="b1" >  <button @click="xiao" >取消</button>
        <button @click="que" >确定</button></p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
name:"List",
data(){
  return{
    list:[],
    flag:false,
    info:[],
    bian:false,
    tan:false,
    arr:[]

  }
},
mounted(){
  //获取json数据
    axios.get("/static/goods.json").then((res)=>{
        // console.log(res)
        this.list=res.data
    })
},
methods:{
  //价格减
  jian(key){
    if( this.list[key].num==0 ){
      return false
    }
    this.list[key].num--
  },
  //价格加
  jia(key){
    this.list[key].num++
  },
  //全选
  xuan(){
    this.flag=!this.flag
    this.list.forEach(item=>{
      item.done=this.flag
      // this.flag=item.done
    })
  },
  //反全选
  onchange(key){
    var ar = this.list[key].done == true
    console.log(ar)
    if (ar) {
        this.info.push(ar)
    }else{
      this.info.splice(key,1)
    }
    if(this.info.length==this.list.length){
      this.flag=true
      }else{
        this.flag=false
      }
  },
  //编辑
  bianji(){
    this.bian=!this.bian
  },
  //删除
  shan(){
      this.tan=!this.tan
  },
  //确定
  que(){
      this.tan=!this.tan
      var tem = this.list.filter((item,key)=>{
       return !item.done
   })
   this.list=tem
   if ( this.list.length==0 ) {
      this.flag=false
   }

   var tem = this.list.filter((item,key)=>{
     return !iitem.done
   })
    
    this.list = tem
   
  },
  //取消
  xiao(){
      this.tan=!this.tan
      this.list.forEach((item,key)=>{
        item.done=false

      })
      this.flag=false
  }
},
computed:{
  //计算总价
  ji(){
    var str = 0
    this.list.forEach((item,key) => {
        if( item.done ){
          str += item.price*item.num 
        }
    });
    return str.toFixed(2)//保留两位小数
  },
  ji(){
    var str = 0
    this.list.forEach((item,key)=>{
      if (item.done) {
        str += item.price*item.num
      }
    }) 
    return str
  },
  asd(){
    var x = 0;
    var str = []
    this.list.forEach(item=>{
      if(item.done==true){
         str.push({"do":item.done})
      }
    })
     x +=str.length
    return x
}
}
}
</script>

<style>
.qw{
  position: relative;
}
.pin {
  width: 100%;
  height: 1.2rem;
  display: flex;
  line-height: 1.2rem;
  border-top: 1px solid #e3e3e3;
  font-size: 0.4rem
}
.pin p:nth-of-type(1){
  width: 0.5rem;
  height: 0.5rem;
  border: 1px solid;
  margin-left: 0.3rem;
  margin-top: 0.32rem;
  border-radius: 50%
}
.pin p:nth-of-type(2){
margin-left: 0.3rem
}
.nei{
  width: 100%;
  height: 2rem;
  border-top: 1px solid #e3e3e3;
  display: flex;
  font-size: 0.28rem

}
.checked{
  width: 10%;
  height: 100%;
  text-align: center;
  line-height: 2rem
}
.img{
  width: 20%;
  height: 100%;
}
.img img{
  width: 100%;
  height: 80%;
}
.yi{
  width: 70%;
  height: 100%;
  line-height: 0.42rem;
  position: relative;
}
.yi p{
  margin-left: 0.2rem
}
.w{
  margin-top: 0.18rem;
  font-size: 0.22rem
}
.q{
  font-size: 0.2rem;
  color: #888888
}
.e{
  color: red
}
.r{
  position: absolute;
  right: 0.1rem;
}
.quan{
  width: 100%;
  height: 1.5rem;
  border-top: 1px solid #e3e3e3;
  display: flex;
  font-size: 0.28rem;
  line-height: 1.5rem;
}
.quan p:nth-of-type(1){
  width: 20%;
  margin-left: 0.2rem
}
.quan p:nth-of-type(2){
  width: 30%;
}
.bian {
  width: 25%;
  height: 100%;
  border: 0px;
  background: #3C8EE4
}
.bian button{
  width: 100%;
  height: 100%;
   border: 0px;
  background: #3C8EE4;
  color: white

}
.quan p:nth-of-type(4){
  width: 25%;
   height: 100%;
 
}
.jie button {
  width: 100%;
  height: 100%;
 border: 0px;
  color: white;
  background: #FE4543
}
.quan span{
  color: red
}
.kuang{
  width: 5rem;
  height: 2.8rem;
  background: white;
  position: absolute;
  top: 50%;
  left: 20%;
  font-size: 0.3rem;
  border-radius: 30px;
  line-height: 0.8rem;
  text-align: center;
}
.bie{
  width: 100%;
  height: 11.5rem;
  position: absolute;
  background: rgba(25, 24, 24, 0.327);
  top:0
}
.b1{
  width: 100%;
  height: 1.3rem;
  /* background: red; */
  display: flex;
  border-top:1px solid #e3e3e3;
}
.b1 button{
  width: 50%;
  height: 100%;
  background: white
}
.b1 button:nth-of-type(1){
  border-bottom-left-radius:  30px;
  border:0px;
  border-right: 1px solid #e3e3e3;
}
.b1 button:nth-of-type(2){
  border-bottom-right-radius:  30px;
  border:0px
}
</style>