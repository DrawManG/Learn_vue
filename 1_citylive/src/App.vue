<template>
  <div>
    <h1>{{ key }}</h1>
    <p>{{ value }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';
import axios from 'axios';

export default defineComponent({
  setup() {
    const key = ref('');
    const value = ref('');

    onMounted(() => {
      fetchData();
    });

    const fetchData = () => {
      axios.get('/json/example.json')
        .then(response => {
          key.value = response.data.key;
          value.value = response.data.value;
        })
        .catch(error => {
          console.log('Ошибка загрузки данных:', error);
        });
    };

    return {
      key,
      value,
      fetchData
    };
  }
});
</script>
