<template>
  <div class="select-dropdown">
    <terms-filter-toggle :id="id" @toggle="togglePanel($event)"></terms-filter-toggle>
    <transition name="slide-fade">
      <div class="select-dropdown-panel card arrow-box" v-show="panelOpen">
        <select-list
          ref="selectList"
          :options="options"
          :selected="selected"
          :id="id"
        >
        </select-list>
      </div>
    </transition>
  </div>
</template>

<script>
  import SelectList from './selectList'
  import TermsFilterToggle from './termsFilterToggle'

  export default {
    name: 'select-drop-down',
    components: {
      SelectList, TermsFilterToggle
    },
    data () {
      return {
        panelOpen: false
      }
    },
    props: ['options', 'selected', 'label', 'placeholder', 'id'],
    methods: {
      togglePanel () {
        this.panelOpen = !this.panelOpen
      }
    }
  }
</script>

