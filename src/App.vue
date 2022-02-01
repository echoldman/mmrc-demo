<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import { ipcRenderer } from 'electron'
import HelloWorld from './components/HelloWorld.vue'

const MMRCRenderer = require('mmrc/renderer')
const mmrc = new MMRCRenderer('mmrc.main.call.method', 'mmrc.renderer.done', 'mmrc.renderer.failed', ipcRenderer)

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted () {
    mmrc.C('hello', 'renderer call main method.').then(message => {
      console.log(message)
    }).catch(error => {
      console.log(error)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
