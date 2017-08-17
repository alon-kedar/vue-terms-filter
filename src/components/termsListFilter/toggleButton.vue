<template>
  <a href="#"
     role="checkbox"
     class="button toggle-button"
     :class="{'is-selected': isSelected}"
     @click="toggle($event)">
    <i class="fa fa-check"></i>
    <span v-html="text"></span>
  </a>
</template>
<script>
  export default {
    name: 'toggle-button',
    data () {
      return {
        isSelected: this.selected ? this.selected : false
      }
    },
    props: ['text', 'selected', 'value'],
    methods: {
      toggle ($event) {
        this.isSelected = !this.isSelected

        this.$emit('toggle', {
          selected: this.isSelected,
          value: this.value
        })
      },
      watch: {
        selected: function (newVal) {
          this.isSelected = newVal
        }
      }
    }
  }
</script>
