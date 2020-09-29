<template>
  <!-- <Header/> -->
  <!-- <Welcome/> -->
  <Menu/>

</template>

<script>
import Header from './components/Header.vue'
import Welcome from './components/welcome.vue'
import Menu from './components/menu.vue'
export default {
  name: 'App',
  components: {
    Menu,
    Header,
    Welcome
  }
}
</script>
<style lang="scss">
body{
   background-image: url('http://subtlepatterns2015.subtlepatterns.netdna-cdn.com/patterns/food.png');
}

// some other scrubs 
// http://www.thegourmetcupcakeshoppe.com/
</style>
