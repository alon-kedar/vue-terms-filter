<template>
  <div>
    <h1 v-text="message"></h1>
    <h2 v-text="msg"></h2>
  </div>
</template>

<script>
  export default {
    name: 'test',
    props: ['msg'],
    data () {
      return {
        message: 'test message'
      }
    }
  }
</script>
