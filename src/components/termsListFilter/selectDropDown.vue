<template>
  <div class="select-dropdown">
    <a href="#"
       role="button"
       class="button is-primary"
       @click="toggle($event)"
    >
      {{buttonText}}
    </a>
    <transition name="slide-fade">
      <div class="select-dropdown-panel card arrow-box" v-show="panelOpen">
        <select-list
          ref="selectList"
          :options="options"
          :selected="selected"
          @change="onChange($event)"
          @filter="onFilterChange($event)"
        >
        </select-list>
      </div>
    </transition>
  </div>
</template>

<script>
  import SelectList from './selectList'

  export default {
    name: 'select-drop-down',
    components: {
      SelectList
    },
    data () {
      return {
        panelOpen: true,
        buttonText: this.label + ' ' + this.placeholder
      }
    },
    props: ['options', 'selected', 'label', 'placeholder'],
    methods: {
      toggle () {
        this.panelOpen = !this.panelOpen
      },
      onChange (event) {
        this.$emit('change', event)
      },
      onFilterChange (event) {
        console.log('yo')
        console.log(event)
        this.setButtonText(event.options)
      },
      setButtonText (selectedOptions) {
        this.buttonText = 'count: ' + selectedOptions.length
      }
    }
  }
</script>


<style>

</style>


