<template>
  <div id="app">
    
    <count-down :endtime="time.endtime" :id="time.id" :servertime="time.servertime"></count-down>

  </div>
</template>

<script>
import CountDown from './components/countdown'

export default {
  data () {
    return {
      time:{
        id:'001',
        servertime:'2015/5/18 11:02:50',
        endtime:'2015/5/18 11:03:20',
      }
    }
  },
  components: {
    CountDown
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 800px;
  min-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
  margin: 0 auto;
}

</style>
