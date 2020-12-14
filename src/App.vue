<template>
  <div id="app">

  <Header />
  
  <Home />

  
 
  </div> 
</template>

<script>

 import Header from './components/layouts/Header';
 import Home from './components/Home';
 


export default {

  name: 'App',

  components: {
    Header,
    Home
    
  },
}

</script>

<style>


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;



}




</style>
