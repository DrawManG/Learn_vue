<template>
    <div class="modal-container">
      <div class="modal-overlay"></div>
      <div class="modal-window">
        <h1>LOCATION COORDINATES</h1>
        <h4 style="text-align: center;"> {{ $props.city }}</h4>
        <p>Location X: {{ $props.x }}</p>
        <p>Location Y: {{ $props.y }}</p>
        <button @click="closeModal">Close</button>
      </div>
    </div>
  </template>
  
  
  <script>
  export default {
    props: {
      x: Number,
      y: Number,
      city: String,
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },
    },
  };
  </script>
  
  <style scoped>
  .modal-container {
    position: relative;
  }
  
  .modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 9998;
  }
  
  .modal-window {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 200px;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    z-index: 9999;
  }
  </style>
  