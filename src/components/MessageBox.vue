<template>
  <div>
    <b-alert variant="success" show><b>{{ message.userName }}:</b> {{ message.text }}</b-alert>
  </div>
</template>

<script>
export default {
  name: 'MessageBox',
  props: {
    message: Object
  }
}
</script>

<style scoped>

</style>