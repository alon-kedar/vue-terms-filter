<template>
  <div id="app">
    <img src="./assets/logo.png">
    <hello></hello>
    <test :msg="'new test.vue message'"></test>
    <terms-list-filter></terms-list-filter>
  </div>
</template>

<script>

import Hello from './components/Hello'
import Test from './components/test'
import TermsListFilter from './components/termsListFilter/termsListFilter'

export default {
  name: 'app',
  components: {
    Hello, Test, TermsListFilter
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
