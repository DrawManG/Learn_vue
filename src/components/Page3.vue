<template>
    <div>
      <button @click="goBack">Go Back</button>
      <button @click="fetchData">Получить данные</button>
  
      <!-- Кнопка для выполнения POST-запроса -->
      <button @click="registerUser">Зарегистрироваться</button>
      <button @click="authorization">Авторизация</button>
      <button @click="showSessions">Показать Сессии</button>
  
      <!-- Отображение полученных данных -->
      <div v-if="serverData">
        <h3>Данные с сервера:</h3>
        <pre>{{ serverData }}</pre>
      </div>
      <div v-if="token">
        Token: {{ token }}
      </div>
      <div v-if="sessionData">
        <div v-for="session in sessionData.data" :key="session.id">
          <button @click="openModal(session)">{{ session.id }} -- {{ session.agent }}</button>
        </div>
      </div>
      <modal3
        :show-modal="showModal"
        :id="modalData.id"
        :id_user="modalData.user.id"
        :login_user="modalData.user.login"
        :name_user="modalData.user.name"
        :agent="modalData.agent"
        :ip="modalData.ip"
        @close-modal="closeModal"
      ></modal3>
    </div>
  </template>
  
  <script>
  import modal3 from '@/components/Modal_Session.vue';
  
  export default {
    data() {
      return {
        currentPage: 'PageTree',
        showModal: false,
        serverData: null,
        token: null,
        sessionData: null,
        modalData: {
          id: null,
          user: {
            id: null,
            login: null,
            name: null,
          },
          agent: null,
          ip: null,
        },
      };
    },
    components: {
      modal3,
    },
    name: 'PageTree',
    methods: {
      openModal(sessionData) {
        this.showModal = true;
        this.modalData.id = sessionData.id;
        this.modalData.user.id = sessionData.user.id;
        this.modalData.user.login = sessionData.user.login;
        this.modalData.user.name = sessionData.user.name;
        this.modalData.agent = sessionData.agent;
        this.modalData.ip = sessionData.ip;
      },
      closeModal() {
        this.showModal = false;
        this.modalData.id = null;
        this.modalData.user.id = null;
        this.modalData.user.login = null;
        this.modalData.user.name = null;
        this.modalData.agent = null;
        this.modalData.ip = null;
      },
      goBack() {
        this.$emit('back');
      },
      fetchData() {
        // Выполнение GET-запроса
        fetch('http://127.0.0.1:3000/')
          .then((response) => response.json())
          .then((data) => {
            this.serverData = data;
          })
          .catch((error) => {
            console.error('Ошибка при выполнении GET-запроса:', error);
          });
      },
      registerUser() {
        const userData = {
          login: 'exampleuser',
          name: 'JohnDoe',
          password: 'examplepassword',
        };
  
        fetch('http://127.0.0.1:3000/api/v1/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(userData),
        })
          .then((response) => response.json())
          .then((data) => {
            this.serverData = data;
          })
          .catch((error) => {
            console.error('Ошибка при выполнении POST-запроса:', error);
          });
      },
      authorization() {
        const userData = {
          login: 'exampleuser',
          password: 'examplepassword',
        };
        fetch('http://127.0.0.1:3000/api/v1/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(userData),
        })
          .then((response) => response.json())
          .then((info) => {
            this.serverData = info;
            this.token = info.data.token;
          })
          .catch((error) => {
            console.error('Ошибка при выполнении POST-запроса:', error);
          });
      },
      showSessions() {
        fetch('http://127.0.0.1:3000/api/v1/sessions', {
          method: 'GET',
          headers: {
            accept: 'application/json',
            Authorization: 'Bearer ' + this.token,
          },
        })
          .then((response) => response.json())
          .then((data) => {
            this.sessionData = data;
          });
      },
    },
  };
  </script>
  
  <style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
  }
  </style>
  