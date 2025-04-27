<template>
    <footer>
      <div class="left">
        <a href="">Accueil</a>
        <a href="">Documents</a>
        <a href="">Portes ouvertes</a>
        <a href="">Cadidature</a>
      </div>
      <div class="left-2">
        <a href="">Mentions légales</a>
        <a href="">Contact</a>
        <a href="">CGU</a>
        <a href="">CGI</a>
      </div>
      <div class="center">
        <p class="brand">Eductive Rennes</p>
        <a href="">14 Rue du bourg Nouveau, 35000 Rennes</a>
        <p> <strong>02 19 13 90 01</strong></p>
        
        <p>Ouvert du <strong>Lundi</strong> au <strong>Vendredi</strong> de <strong>8h</strong> à <strong>18h</strong></p>
      </div>
      <div class="nav-buttons">
        <button class="inscr">Inscription</button>
        <button class="po">Portes ouvertes</button>
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
  .brand {
    font-size: 35px;
    font-weight: bold;
  }

  .left, .left-2 {
    display: flex;
    flex: 1;
    flex-direction: column;
    align-items: start;
    text-align: start;
  }
  .left {
    margin-right: 20px;
  }
  
  .logo img {
    max-height: 40px;
  }
  .nav-buttons {
    display: flex;
    flex-direction: column;
  }
  .nav-buttons button {
    border: none;
    margin-left: 20px;
    cursor: pointer;
    margin-bottom: 10px;
  }
  .center {
    flex: 12;
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
    background-color: #7009fb;
    color: white;
    border-radius: 5px;
    padding: 10px 20px;
    transition: background-color 0.3s ease;
    }
  </style>
  