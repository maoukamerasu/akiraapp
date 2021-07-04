<template>
  <div id="app">
    <table border="1" align="center">
      <tr bgcolor="cc3366"><font size="6" color="000000">オセロ</font></tr>
      <tr bgcolor="ffffff">
    <Othello/>
    </tr>
    </table><br>
    <table border="1" align="center">
    <tr bgcolor="666600"><font size="6" color="000000">スライム</font></tr>
    <tr bgcolor="ffffff">
    <Slime />
    </tr>
    </table><br>
    <table border="1" align="center">
    <tr bgcolor="666600"><font size="6" color="000000">電卓</font></tr>
    <tr bgcolor="ffffff">
    <Convenient />
    </tr>
    </table>
  </div>
</template>

<script>
import Othello from './components/Othello.vue'
import Slime from './components/Slime.vue'
import Convenient from './components/Convenient.vue'

export default {
  name: 'App',
  components: {
    Othello,Slime,Convenient
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
  margin-top: 0px;
  background-color:#333399
}
</style>
