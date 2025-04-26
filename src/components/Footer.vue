<template>
    <footer>
      <div class="logo">
        <img src="/public/vite.svg" alt="Logo">
      </div>
      <div class="nav-buttons">
        <button>Accueil</button>
        <button>À propos</button>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'Nav'
  }
  </script>
  
  <style scoped>
  footer {
    height: 30vh;
  background-image: url('/public/eductive-png.png');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  width: 98vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  color: black;
  padding: 10px 20px;
  }
  
  .logo img {
    max-height: 40px;
  }
  
  .nav-buttons button {
    background-color: transparent;
    color: black;
    border: none;
    margin-left: 20px;
    cursor: pointer;
  }
  </style>
  