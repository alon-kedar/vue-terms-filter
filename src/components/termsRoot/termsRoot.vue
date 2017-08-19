<template>
  <div>
    <div class="root-actions">
      <button class="btn btn-default" @click="sort()">Sort</button>
      <button class="btn btn-default" @click="removeDuplicates()">Clean</button>
    </div>
    <p class="root-count" v-text="'count:' + terms.length"></p>
    <textarea class="form-control text-area-root" cols="38" rows="10" v-model="inputText" placeholder=" Add terms"></textarea>
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
    methods: {
      sort () {
        this.terms = this.terms.sort((a, b) => a.localeCompare(b))
      },
      removeDuplicates () {
        this.terms = Array.from(new Set(this.inputText.split('\n').map((t) => t.trim()).filter((t) => t !== '')))
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
    computed: {

      terms: {
        get () {
          return Array.from(new Set(this.inputText.split('\n').map((t) => t.trim()).filter((t) => t !== '')))
        },
        set (terms) {
          this.inputText = terms.join('\n')
        }
      }
    },
    watch: {
      inputText: function (text) {
        EventBus.$emit('updateTerms' + this.id, this.terms)
      }
    }
  }
</script>

<style>
  .text-area-root {
    margin: auto;
    width: 300px;
  }
  .root-count {
    color: #3572b0;
    text-decoration: underline;
  }
  .root-actions {
    display: flex;
    flex-direction: column;
    width: 60px;
    position: absolute;
    right: 450px;
    top: 70px;
  }

  .root-actions .btn {
    margin-bottom: 10px!important;
  }
</style>
