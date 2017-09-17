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
      greeting: 'Vamailteeth'
    }
  }
}
</script>
<style>
body {
  background-image:url("/static/img/trees_bg.png");
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 2em;
}

#app h1 {
  text-align: center;
  color: #CEF0D4;
  font-family: 'Rouge Script', cursive;
  font-size: 5em;
  font-weight: normal;
  line-height: 1em;
  margin: 0 0 50px;
  text-align: center;
  text-shadow: 1px 1px 2px #082b34;
  position: absolute;
  left: 10em;
  top: 0.2em;
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
