<template>
  <div id="app">
    <HelloWorld/>
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
}

#disqus_thread {
  margin-top: 30px;
  margin-right: 5%;
  margin-left: 5%
}
</style>
