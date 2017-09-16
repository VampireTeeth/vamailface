<template>
  <div id="app">
    <h1>{{ greeting }}</h1>
    <mail></mail>
  </div>
</template>

<script>
import Mail from './components/Mail'

export default {
  name: 'App',
  components: { Mail },
  data () {
    return {
      greeting: 'Welcome to Vamailteeth'
    }
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

.grouping:before,
.grouping:after {
  content: "";
  display: table;
}

.grouping:after {
  clear: both;
}

</style>
