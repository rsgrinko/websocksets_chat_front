<template>
  <div>
    <b-list-group style="max-width: 300px;" class="mb-4 mt-4">

      <b-list-group-item class="d-flex align-items-center" v-for="user in userList" v-bind:key="user.userId">
        <b-avatar class="mr-3"></b-avatar>
        <span class="mr-auto">{{ user.userName }}</span>
      </b-list-group-item>

    </b-list-group>
  </div>
</template>

<script>
export default {
  name: 'UsersList',
  props: {
    userList: Array
  }
}
</script>

<style scoped>

</style>