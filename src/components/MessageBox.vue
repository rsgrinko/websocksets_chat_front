<template>
  <div>
    <div v-for="message in messages" v-bind:key="message.text">
      <b-alert v-if="!message.system" variant="success" show><b>{{ message.from }}[{{ message.userId }}]:</b> {{ message.text }}</b-alert>
      <b-alert v-else variant="info" show>{{ message.text }}</b-alert>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageBox',
  props: {
    messages: Array
  }
}
</script>

<style scoped>

</style>