<template>
  <div id="app">
    <img src="./assets/logo.png">
    <hello></hello>
    <test :msg="'new test.vue message'"></test>
    <terms-list-filter></terms-list-filter>
    <terms-root></terms-root>
  </div>
</template>

<script>

import Hello from './components/Hello'
import Test from './components/test'
import TermsListFilter from './components/termsListFilter/termsListFilter'
import TermsRoot from './components/termsRoot/temsRoot'

export default {
  name: 'app',
  components: {
    Hello, Test, TermsListFilter, TermsRoot
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
