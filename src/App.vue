<template>
  <div id="app">
    <Header></Header>
    <div class="content" >
         <router-view/> 
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  components:{Header,Footer},
  name: 'App'
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
#app{
  display: flex;
  flex-direction: column;
}
.content{
  width: 100%;
  flex: 1;
  overflow: auto;
}
</style>
