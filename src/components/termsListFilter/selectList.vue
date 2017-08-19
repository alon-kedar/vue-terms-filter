<template>
  <div class="select-list-wrapper">
    <header class="select-list-actions is-clearfix">
      <p>
        <input class="input" v-model="filterText" type="text" placeholder="Filter list">
      </p>
      <button type="button" class="button is-link" :disabled="selectedOptions.length === 0"
              v-clipboard:copy="selectedOptionsStr">Copy</button>
      <button type="button" class="button is-link" :disabled="selectedOptions.length === 0"
              v-clipboard:copy="selectedOptionsStr"
              @click="remove()">Cut</button>
    </header>
    <div class="select-list" v-if="filteredOptions.length > 0">
      <form>
        <select v-model="selectedOptions" class="multipass form-control" v-bind:size="filteredOptions.length" multiple>
          <option v-for="option in filteredOptions" v-text="option" v-bind:value="option"></option>
        </select>
      </form>
    </div>
    <div v-else>No terms to display</div>
  </div>
</template>

<script>
  import EventBus from './../../eventBus'
  import ToggleButton from './toggleButton'

  export default {
    name: 'select-list',
    components: {
      ToggleButton
    },
    data () {
      return {
        filterText: '',
        selectedOptions: [],
        copyData: 'some data'
      }
    },
    props: ['options', 'selected', 'id'],
    methods: {
      onToggle (option) {
        if (option.selected) {
          this.selectedOptions.push(option.value)
        } else {
          this.selectedOptions.splice(this.selectedOptions.indexOf(option.value), 1)
        }
        this.$emit('change', {
          changed: option,
          selected: this.selectedOptions
        })
      },
      remove () {
        EventBus.$emit('removeTerms', this.selectedOptions)
        this.selectedOptions = []
      }
    },
    computed: {
      filteredOptions () {
        let filterText = this.filterText ? this.filterText.trim().toLocaleLowerCase() : ''
        return this.options.filter((option) => option.trim().toLocaleLowerCase().includes(filterText))
      },
      selectedOptionsStr () {
        return this.selectedOptions.join('\n')
      }
    },
    watch: {
      filterText () {
        EventBus.$emit('updateTerms' + this.id, this.filteredOptions)
      }
    },
    mounted () {
      EventBus.$on('filterWasAdded' + (this.id + 1), () => {
        EventBus.$emit('updateTerms' + this.id, this.filteredOptions)
      })
    }
  }
</script>

<style>
  select{
    width: 300px;
    max-height: 200px;
  }
</style>
