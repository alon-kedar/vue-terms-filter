<template>
  <div>
    <textArea v-text="inputText" @input="updateTerms($event.target.value)"></textArea>
  </div>
</template>


<script>
  import EventBus from './../../eventBus'

  export default {
    name: 'terms-root',
    data () {
      return {
        inputText: '',
        terms: []
      }
    },
    methods: {
      updateTerms (text) {
        this.terms = text.split('\n').map((t) => t.trim()).filter((t) => t !== '')
        EventBus.$emit('updateTerms', this.terms)
      }
    }
  }
</script>
