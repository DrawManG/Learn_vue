<template>
  <div>
    <div v-for="(location, city) in locationData" :key="city">
      <button style="width: 99%; height: 50px;" @click="openModal(location.lat, location.lng,city)">{{ city }}</button>
    </div>
    <div v-if="showModal" class="modal-overlay">
      <ModalWindow :x="modalX" :y="modalY" :city="city" @close="closeModal" />
    </div>
  </div>
</template>

<script>
import ModalWindow from './components/ModalWindow.vue';
import locationData from './assets/users.json';

export default {
  components: {
    ModalWindow,
  },
  data() {
    return {
      locationData: locationData,
      showModal: false,
      modalX: null,
      modalY: null,
      city: null,
    };
  },
  methods: {
    openModal(x, y,city) {
      this.showModal = true;
      this.modalX = x;
      this.modalY = y;
      this.city = city;
    },
    closeModal() {
      this.showModal = false;
      this.modalX = null;
      this.modalY = null;
      this.city = null;
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
