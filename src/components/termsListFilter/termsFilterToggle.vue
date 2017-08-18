<template>
  <a href="#"
     role="button"
     class="button is-primary"
     @click="toggle()"
     v-text="buttonText"
  >
  </a>
</template>

<script>
  import EventBus from './../../eventBus'

  export default {
    name: 'terms-filter-toggle',
    data () {
      return {
        filteredTermsCount: 0
      }
    },
    methods: {
      toggle () {
        this.$emit('toggle')
      }
    },
    computed: {
      buttonText () {
        return 'count: ' + this.filteredTermsCount
      }
    },
    mounted () {
      EventBus.$on('visibleOptionsUpdated', (options) => {
        this.filteredTermsCount = options.length
      })
    }
  }
</script>
