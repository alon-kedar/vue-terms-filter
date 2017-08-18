<template>
  <div class="select-list-wrapper">
    <header class="select-list-actions is-clearfix">
      <p class="control">
        <input class="input" v-model="filterText" type="text" placeholder="Filter list">
      </p>
      <p class="control" v-if="selectedOptions.length > 0">
        <a href="#" role="button" class="button is-link" @click="remove"> Remove selected </a>
      </p>
    </header>
    <div class="select-list" v-if="filteredOptions.length > 0">
      <toggle-button
        v-for="option in filteredOptions"
        :text="option.label"
        :value="option.value"
        :selected="option.selected"
        class="select-item"
        @toggle="onToggle($event)"
      ></toggle-button>
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
        selectedOptions: this.selected
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
        let visibleOptions = []
        let filterText = this.filterText.trim().length > 0 ? this.filterText.toLowerCase() : null

        if (filterText) {
          visibleOptions = this.options.filter((option) => {
            let optWords = option.split(' ')
            return optWords.some((word) => {
              return word.toLowerCase().indexOf(filterText) === 0
            })
          })
        } else {
          visibleOptions = this.options
        }

        return visibleOptions.map((option) => {
          let label = ''

          if (filterText) {
            let searchStartIndex = option.toLowerCase().indexOf(filterText)
            let filterPart = option.substring(searchStartIndex, searchStartIndex + filterText.length)
            label = option.replace(filterPart, `<b>${filterPart}</b>`)
          } else {
            label = option
          }

          return {
            value: option,
            label,
            selected: this.selectedOptions.includes(option)
          }
        })
      },
      thingsToWatch () {
        return [{a: this.filterText}, {b: this.options}]
      }
    },
    watch: {
      thingsToWatch: {
        handler: function () {
          this.visibleOptions = this.filteredOptions.map((o) => o.value)
          EventBus.$emit('visibleOptionsUpdated', this.visibleOptions)
          EventBus.$emit('updateTerms' + this.id, this.visibleOptions)
        },
        deep: true
      }
    },
    mounted () {
      EventBus.$on('filterWasAdded' + (this.id + 1), () => {
        EventBus.$emit('updateTerms' + this.id, this.visibleOptions)
      })
    }
  }
</script>
