<template>
  <div id="app">
    <div  v-show="isShow">
      <img alt="Vue logo" src="./assets/abc.png">
      <h1>Welcome tây vương mẫu</h1>
    </div>
    <hr/>
    <button @click="isShow = !isShow">Show/Hide</button>
    <hr/>
    <input type="text" :disabled="inputDisable"/>
    <button @click="inputDisable = ! inputDisable">Lock/Unlock</button>
    
    <Test />
  </div>
</template>

<script>
  import Test from './components/Test.vue'

  export default {
    name : 'App',
    components : {
      Test
    },
    data() {
      return {
        isShow : true,
        inputDisable : true
      }
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
