<template>
  <div id="app">
    <multi-form></multi-form>
  </div>
</template>

<script>
import MultiForm from './components/MultiForm';

export default {
  name: 'app',
  components: {
    MultiForm
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
