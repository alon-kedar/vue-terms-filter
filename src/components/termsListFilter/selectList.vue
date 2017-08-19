<template>
  <div class="select-list-wrapper">
    <button type="button"
            v-clipboard:copy="selectedOptionsStr">Copy!</button>
    <header class="select-list-actions is-clearfix">
      <p class="control">
        <input class="input" v-model="filterText" type="text" placeholder="Filter list">
      </p>
      <p class="control" v-if="selectedOptions.length > 0">
        <a href="#" role="button" class="button is-link" @click="remove"> Remove selected </a>
      </p>
    </header>
    <div class="select-list" v-if="filteredOptions.length > 0">
      <form>
        <select v-model="selectedOptions" class="multipass" v-bind:size="filteredOptions.length" multiple>
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
        console.log(this.selectedOptions)
        return this.selectedOptions.join('\n')
      },
      thingsToWatch () {
        return [{a: this.filterText}, {b: this.filteredOptions}]
      }
    },
    watch: {
      thingsToWatch: {
        handler: function () {
          EventBus.$emit('updateTerms' + this.id, this.filteredOptions)
        },
        deep: true
      },
      copyData: function () {
        console.log(this.copyData)
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
