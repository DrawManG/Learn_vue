<template>
    <div>
      
      <button @click="goBack">Go Back</button>
    </div>
    <div>
        <p></p>
        <input type="text" v-model="searchFilm" placeholder="Поиск фильма" />
        <p>_______________________________________________________________________________</p>
        <div v-for="film in filteredFilm" :key="film.title">
            <div>
            <p>{{ film.title }}</p>
                <p>{{ film.year }}</p>
        <p>{{ film.description }}</p>
        <p>_______________________________________________________________________________</p>
            </div>
        </div>
      
    </div>
  </template>
  
  <script>
  import filmdata from '@/assets/films.json';
  
  export default {
    data() {
      return {
        filmdata: filmdata,
        searchFilm: '',
      };
    },
    name: 'PageTwo',
    methods: {
      goBack() {
        this.$emit('back');
      },
    },
    computed: {
      filteredFilm() {
        if (!this.searchFilm) {
          return this.filmdata;
        }
        const searchQuery = this.searchFilm.toLowerCase();
        return Object.values(this.filmdata).reduce((filtered, film) => {
          if (film.title.toLowerCase().includes(searchQuery)) {
            filtered[film.title] = film;
          }
          return filtered;
        }, {});
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
  
  