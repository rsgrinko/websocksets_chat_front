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
            <MessageBox :messages="messages"/>
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
      connection: null,
      messages: [],
      userList: [],
    }
  },
  created: function () {
    this.connection = new WebSocket('wss://dev.it-stories.ru/wss?userName=Guest_anonimous')
    const vueObject = this;
    this.connection.onmessage = function (event) {
      let data = JSON.parse(event.data);

      // Обработка пингов
      if (data.action === 'Ping') {
        const pongMessage = {action: 'Pong'};
        vueObject.connection.send(JSON.stringify(pongMessage));
      }

      // Обработка сообщений
      if (data.action === 'PublicMessage') {
        console.log(data);
        vueObject.messages.push(
            {system: false, from: data.userName, text: data.text, userId: data.userId}
        );
        if (vueObject.messages.length >= 10) {
          vueObject.messages = vueObject.messages.slice(1);
        }
      }

      // Обработка при авторизации
      if (data.action === 'Authorized') {
        vueObject.userList = data.users;
      }

      // Обработка при подключении
      if (data.action === 'Connected') {
        vueObject.messages.push(
            {system: true, from: "system", text: `Пользователь ${data.userName} подлючился в чат`, userId: null}
        );
        if (vueObject.messages.length >= 10) {
          vueObject.messages = vueObject.messages.slice(1);
        }
      }

      // Обработка при отключении
      if (data.action === 'Disconnected') {
        vueObject.messages.push(
            {system: true, from: data.userName, text: `Пользователь ${data.userName} покинул чат`, userId: data.userId}
        );
        if (vueObject.messages.length >= 10) {
          vueObject.messages = vueObject.messages.slice(1);
        }
        vueObject.userList = data.users;
      }

      // Обработка информационных сообщений
      if (data.action === 'Information') {
        vueObject.messages.push(
            {system: true, from: "system", text: data.text, userId: null}
        );
        if (vueObject.messages.length >= 10) {
          vueObject.messages = vueObject.messages.slice(1);
        }
      }
    }

    this.connection.onopen = function () {
      vueObject.messages.push(
          {system: true, from: "system", text: "Соединение установлено", userId: null}
      );
      if (vueObject.messages.length >= 10) {
        vueObject.messages = vueObject.messages.slice(1);
      }
    }

    this.connection.onclose = function (event) {
      let message;
      if (event.wasClean) {
        message = `Соединение закрыто чисто, код=${event.code} причина=${event.reason}`;
      } else {
        message = "Соединение прервано";
      }

      vueObject.messages.push(
          {system: true, from: "system", text: message, userId: null}
      );
      if (vueObject.messages.length >= 10) {
        vueObject.messages = vueObject.messages.slice(1);
      }
    }

  },
  methods: {
    sendMessage: function (message) {
      this.connection.send(message);
    }
  },
}
</script>

<style>

</style>
