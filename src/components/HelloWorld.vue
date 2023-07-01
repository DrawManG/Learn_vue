<template>
  <p v-for="user in users" :key="user.key">
    {{user.value}}
  </p>
</template>

<script>
import userData from './assets/users.json'

export default {
  data() {
    return {
      users: userData,
    };
  },
};
</script>