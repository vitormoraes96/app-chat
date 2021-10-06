<template>
  <div id="app">
    <nav class="nav">
      <h1>APP CHAT</h1>
    </nav>
      <div class="chat" >
         <Chat/>
      </div>
  </div>
</template>

<script>

import Chat from './components/Chat.vue'
export default {
  name: 'App',
  components: {
    Chat
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

  
}
.nav{
  background: #4BC7EE;
  font-family: sans-serif;
  font-weight: bold;
  font-size: 50px;
  margin-top: -60px;
  color: white;
  width: 98vw;
  border: none;
  border-radius: 4px;
}
.chat{
  width: 100vw;
  height: 100vh;
}
</style>
