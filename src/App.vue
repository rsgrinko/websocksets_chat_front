<template>
  <div id="app">
    <TopNavbar infoMessage="test"/>
    <div>

      <b-row>
        <b-col>
          <UsersList :userList="userList"/>
        </b-col>
        <b-col cols="10">
          <div class="mt-4 w-75">
            <MessageBox :message="postTest"/>
            <!--<HelloWorld msg="Hello boba"/>-->
          </div>
        </b-col>
      </b-row>
      <InputFields/>
    </div>


  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import TopNavbar from './components/TopNavbar.vue'
import InputFields from './components/InputFields.vue';
import UsersList from './components/UsersList.vue';
import MessageBox from './components/MessageBox.vue';

export default {
  name: 'App',
  components: {
    //HelloWorld,
    TopNavbar,
    InputFields,
    UsersList,
    MessageBox
  },
  data() {
    return {
      aspect: '16:9',
      userList: [
        {id: 1, name: "Bob"},
        {id: 2, name: "Kate"},
        {id: 3, name: "John Snow"},
      ],
      postTest: {text: "test", userName: "Roman"}
    }
  }
}

setInterval(function () {

}, 1000);
</script>

<style>

</style>
