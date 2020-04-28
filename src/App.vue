<template>
  <div id="app">
    <HelloWorld/>
    <div id="disqus_thread"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gaegu:wght@400;700&display=swap');
#app {
  font-family: 'Gaegu', cursive;  
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

#disqus_thread {
  margin-top: 30px;
  margin-right: 10%;
  margin-left: 10%
}
</style>
