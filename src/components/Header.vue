<template>
    <header class="headerContainer">
      <div class="logoContainer">
        <img src="../logo.png" alt="Logo" class="logo" />
        <h1 class="title">Traverse</h1>
      </div>
    
        <CitySelector
            :onCitySelected="onCitySelected"
            :onSearchNearby="onSearchNearby"
        />
     
    </header>
  </template>
  
  <script>
  import CitySelector from './CitySelector.vue';

  export default {
    name: 'Header',
    components: {
        CitySelector
    },
    props: {
      onCitySelected: Function,
      onSearchNearby: Function
    }
  };
  </script>
  
  <style scoped>
  .headerContainer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: linear-gradient(135deg, #ff6b6b, #4ecdc4);
    color: #ffffff;
    padding: 20px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .logoContainer {
    display: flex;
    align-items: center;
  }
  
  .logo {
    width: 60px;
    margin-right: 10px;
  }
  
  .title {
    margin: 0;
    font-size: 35px;
    font-weight: bold;
  }
  </style>
  