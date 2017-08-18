<template>
  <div>
    <select-drop-down
      :options="terms"
      :selected="selectedTerms"
      :id="id"
      @change="onChange($event)"
      label="Select"
      placeholder="None"
      class=""
    >
    </select-drop-down>
  </div>
</template>

<script>
  import EventBus from './../../eventBus'
  import SelectDropDown from './selectDropDown'
  import ToggleButton from './toggleButton'

  export default {
    name: 'terms-list-filter',
    components: {
      SelectDropDown, ToggleButton
    },
    props: ['id'],
    data () {
      return {
        terms: [],
        selectedTerms: []
      }
    },
    methods: {
      onChange (changed) {}
    },
    mounted () {
      EventBus.$on('updateTerms' + (this.id - 1), (terms) => {
        this.terms = terms
        EventBus.$emit('updateTerms' + this.id, this.terms)
      })
      EventBus.$on('filterWasAdded' + (this.id + 1), () => {
        EventBus.$emit('updateTerms' + this.id, this.terms)
      })
      EventBus.$emit('filterWasAdded' + this.id, {})
    }
  }
</script>

<style>
  .select-dropdown {
    position: relative;
  }
  .select-dropdown {
    position: relative;
  }
  .select-dropdown .select-dropdown-panel {
    width: 360px !important;
    margin: auto;
    /*max-width: 760px;*/
    /*position: absolute;*/
    /*top: calc(100% + 5px);*/
    /*left: calc(50%);*/
    /*transform: translateX(-50%);*/
  }
  .select-dropdown .button.is-primary,
  .button.is-info {
    margin: 15px 0;
  }
  .select-dropdown .select-list-wrapper {
    padding: 10px 10px;
  }
  .select-dropdown .select-list-actions {
    padding: 0 10px 10px;
    margin-bottom: 10px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: flex-start;
  }
  .select-dropdown .select-list-actions .button.is-link {
    color: #7a7a7a;
    text-decoration: none;
    margin-right: 10px !important
  }
  .select-dropdown .select-list {
    margin-top: 10px;
  }
  .select-dropdown .select-item {
    flex-basis: 20%;
    margin-bottom: 1%;
  }
  .select-dropdown .toggle-button {
    background: none;
    color: #7a7a7a;
    border: none;
    padding-left: 25px;
    position: relative;
    margin-left: 0 !important;
    transition: font-weight .1s ease-in;
  }
  .select-dropdown .toggle-button:focus {
    box-shadow: none;
  }
  .select-dropdown .toggle-button.is-selected {
    color: #00D1B2;
  }
  .select-dropdown .toggle-button.is-selected .fa {
    opacity: 1;
  }
  .select-dropdown .toggle-button .fa {
    /*position: absolute;*/
    /*left: 7px;*/
    font-size: 12px;
    opacity: 0;
    transition: opacity .1s ease-in;
  }
  .select-dropdown .arrow-box:after,
  .select-dropdown .arrow-box:before {
    bottom: 100%;
    left: 50%;
    border: solid transparent;
    content: " ";
    height: 0;
    width: 0;
    position: absolute;
    pointer-events: none;
  }
  .select-dropdown .arrow-box:after {
    border-color: rgba(255, 255, 255, 0);
    border-bottom-color: #fff;
    border-width: 7px;
    margin-left: -7px;
  }
  .select-dropdown .arrow-box:before {
    border-color: rgba(234, 234, 234, 0);
    border-bottom-color: #cecece;
    border-width: 8px;
    margin-left: -8px;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
  }

  .slide-fade-leave-active {
    transition: all .1s ease;
  }

  .slide-fade-enter, .slide-fade-leave-active {
    transform: translateY(20px);
    opacity: 0;
  }
</style>
