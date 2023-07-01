<template>
    <div>
      <h1>{{ key }}</h1>
      <p>{{ value }}</p>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  
  export default defineComponent({
    data() {
      return {
        key: '',
        value: ''
      };
    },
    created() {
      this.fetchData();
    },
    methods: {
      fetchData() {
        fetch('/json/example.json')
          .then(response => response.json())
          .then(data => {
            this.key = data.key;
            this.value = data.value;
          })
          .catch(error => {
            console.log('Ошибка загрузки данных:', error);
          });
      }
    }
  });
  </script>
  