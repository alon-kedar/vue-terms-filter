<template>
  <div>
    <textarea cols="42" rows="10" v-model="inputText" placeholder=" Add terms"></textarea>
  </div>
</template>

<script>
  import EventBus from './../../eventBus'

  export default {
    props: ['id'],
    name: 'terms-root',
    data () {
      return {
        inputText: ''
      }
    },
    mounted () {
      EventBus.$on('removeTerms', (terms) => {
        let termsSet = new Set(this.terms)
        terms.forEach((t) => termsSet.delete(t))
        this.terms = Array.from(termsSet)
        this.inputText = this.terms.join('\n')
      })
    },
    watch: {
      inputText: function (text) {
        this.terms = this.inputText.split('\n').map((t) => t.trim()).filter((t) => t !== '')
        EventBus.$emit('updateTerms' + this.id, this.terms)
      }
    }
  }
</script>
