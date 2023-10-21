<template>
  <dance-floor :boysList="boysList" :girlsList="girlsList"/>
</template>

<script>
import DanceFloor from './components/DanceFloor.vue'
import {boysList, girlsList } from './constants/10_dancing_pair'

export default {
  name: 'App',
  components: {
    DanceFloor   
  },

  data() {
    return {
      boysList,
      girlsList,
    }
  },
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
