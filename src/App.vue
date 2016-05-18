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
        servertime:'2015/05/18 11:54:59', 
        endtime:'2015/05/18 11:55:00',
      }
    }
  },
  components: {
    CountDown
  },
  // 在创建实例时 `events` 选项简单地调用 `$on`
  events: {
    'callback' (msg) {
      // 事件回调内的 `this` 自动绑定到注册它的实例上
      console.log('收到消息了')
    }
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
