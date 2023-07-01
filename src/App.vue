<template>
  <div>
    <div>
  
</div>
    <div v-if="currentPage === 'App'">
      <input type="text" v-model="searchCity" placeholder="Поиск города" />
      
      <div v-for="(location, city) in filteredLocationData" :key="city">
        <button style="width: 99%; height: 50px;" @click="openModal(location.lat, location.lng, city)">{{ city }}</button>
      </div>
      <button @click="goToPage2">Go to Page 2</button>
    </div>
    <div v-else-if="currentPage === 'Page2Vue'">
      <Page2Vue @back="goBackToApp" />
    </div>
    <div v-if="showModal" class="modal-overlay">
      <ModalWindow :x="modalX" :y="modalY" :city="city" @close="closeModal" />
    </div>
  </div>
</template>

<script>
import ModalWindow from './components/ModalWindow.vue';
import locationData from './assets/users.json';
import Page2Vue from './components/Page2.vue';

export default {
  components: {
    ModalWindow,
    Page2Vue,
  },
  data() {
    return {
      locationData: locationData,
      showModal: false,
      modalX: null,
      modalY: null,
      city: null,
      currentPage: 'App',
      searchCity: '',
    };
  },
  methods: {
    goToPage2() {
      this.currentPage = 'Page2Vue';
    },
    goBackToApp() {
      this.currentPage = 'App';
    },
    openModal(x, y, city) {
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
  computed: {
  filteredLocationData() {
    if (!this.searchCity) {
      return this.locationData;
    }
    const searchQuery = this.searchCity.toLowerCase();
    return Object.entries(this.locationData).reduce((filtered, [city, location]) => {
      if (city.toLowerCase().includes(searchQuery)) {
        filtered[city] = location;
      }
      return filtered;
    }, {});
  },
}

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
