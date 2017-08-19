<template>
  <div id="app">
    <terms-root :id="0"></terms-root>
    <terms-list-filter v-for="count in filtersCount" :id="count"></terms-list-filter>
    <button class="btn btn-primary" @click="add()">Add filter</button>
  </div>
</template>

<script>

import TermsListFilter from './components/termsListFilter/termsListFilter'
import TermsRoot from './components/termsRoot/termsRoot'

export default {
  name: 'app',
  data () {
    return {
      filtersCount: 2,
      filteredTerms: []
    }
  },
  methods: {
    add () {
      this.filtersCount++
    }
  },
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
  margin-top: 20px;
}
</style>
