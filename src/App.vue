<template>
  <div id="app">
      <h1>Notas</h1>
        <br>

        <Navbar />
        <router-view></router-view>

  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>

</style>
