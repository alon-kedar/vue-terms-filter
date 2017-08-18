<template>
  <div>
    <textarea cols="54" rows="10" v-model="inputText" placeholder="add terms"></textarea>
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
    mounted () {
      EventBus.$on('removeTerms', (terms) => {
        let termsSet = new Set(this.terms)
        terms.forEach((t) => termsSet.delete(t))
        console.log(termsSet)
        this.terms = Array.from(termsSet)
        this.inputText = this.terms.join('\n')
      })
    },
    watch: {
      inputText: (text) => {
        this.terms = text.split('\n').map((t) => t.trim()).filter((t) => t !== '')
        EventBus.$emit('updateTerms', this.terms)
      }
    }
  }
</script>
