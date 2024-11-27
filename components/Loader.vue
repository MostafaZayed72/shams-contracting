<template>
    <div class="loader">
      <img src="https://mir-s3-cdn-cf.behance.net/project_modules/1400/c0b63289239975.5deed8161b1e5.jpg" class="spinner" alt="logo" />
    </div>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  .loader {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(10, 91, 138, 0.247);
    /* خلفية شفافة */
    z-index: 9999;
  }
  
  
  
  .spinner {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    animation: spin 2s linear infinite;
  }
  
  @keyframes spin {
    100% {
      transform: rotate(360deg);
    }
  }
  </style>