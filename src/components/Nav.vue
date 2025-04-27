<template>
    <nav>
      <div class="logo">
        <img src="/public/eductive-grey.png" alt="Logo">
      </div>
      <div class="nav-buttons">
        <button class="inscr">Inscription</button>
        <button class="po">Portes ouvertes</button>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'Nav'
  }
  </script>
  
  <style scoped>
  nav {
    display: flex;

    width: 98vw;
    z-index: 1;
    justify-content: space-between;
    align-items: center;
    background-color: #f6f0ff;
    color: black;
    padding: 10px 20px;
  }
  
  .logo img {
    max-height: 40px;
  }
  
  .nav-buttons button {

    border: none;
    margin-left: 20px;
    cursor: pointer;
  }
  .inscr {
    background-color: #f8cfd4;
    color: black;
    border-radius: 5px;
    padding: 10px 20px;
    transition: background-color 0.3s ease;
  }
  .inscr:hover, .po:hover {
    background-color: #fcb33a;
  }
  .po { 
      transition: background-color 0.3s ease;
        background-color: #7009fb;
        color: white;
        border-radius: 5px;
        padding: 10px 20px;
    }
  </style>
  