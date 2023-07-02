<template>
  <div class="modal-overlay" v-if="showModal">
    <div class="modal-window">
      <p>ID PC: {{ id }}</p>
      <p>ID USER: {{ id_user }}</p>
      <p>LOGIN USER: {{ login_user }}</p>
      <p>NAME USER: {{ name_user }}</p>
      <p>AGENT CONNECT: {{ agent }}</p>
      <p>IP: {{ ip }}</p>
      <button @click="closeModal">Cancel</button>
      <button>Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: String,
    id_user: String,
    login_user: String,
    name_user: String,
    agent: String,
    ip: String,
    showModal: Boolean,
  },
  methods: {
    closeModal() {
      this.$emit('close-modal');
    },
  },
};
</script>

<style scoped>
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

.modal-window {
  background-color: #fff;
  padding: 20px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
