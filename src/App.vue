<template>
  <div id="app">
    <terms-root></terms-root>
    <terms-list-filter></terms-list-filter>
  </div>
</template>

<script>

import TermsListFilter from './components/termsListFilter/termsListFilter'
import TermsRoot from './components/termsRoot/termsRoot'

export default {
  name: 'app',
  components: {
    TermsListFilter, TermsRoot
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
