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
    props: ['id'],
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
      EventBus.$on('visibleOptionsUpdated' + this.id, (options) => {
        this.filteredTermsCount = options.length
      })
    }
  }
</script>
