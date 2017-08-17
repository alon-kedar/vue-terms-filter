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
        this.setButtonText(event.selected)
        this.$emit(event)
      },
      setButtonText (selectedOptions) {
        if (selectedOptions.length === 0) {
          this.buttonText = this.label + ' ' + this.placeholder
        } else {
          let text = this.placeholder.charAt(0).toUpperCase() + this.placeholder.slice(1) + ': ' + selectedOptions[0]

          if (selectedOptions.length > 1) {
            text += ' & ' + (selectedOptions.length - 1) + ' more'
          }

          this.buttonText = text
        }
      }
    }
  }
</script>


<style>

</style>


