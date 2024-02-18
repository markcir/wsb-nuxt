<template>
  <div id="app">
    <nav>
      <ul>
        
        <nuxt-link to="/"><img src="../img/logo.png" alt="Logo" style="width: 40px; height: 40px; margin: 0px; padding: 0px;"></nuxt-link>
        <li><nuxt-link to="/">Home</nuxt-link></li>
        <li><nuxt-link to="Termins">Terminy</nuxt-link></li>
        <li><nuxt-link to="About">O nas</nuxt-link></li>
        <li><nuxt-link to="AppAPI">API(CoinGecko)</nuxt-link></li>
        
        <li style="margin-left: auto;"><nuxt-link to="Auth">Logowanie/Rejestracja</nuxt-link></li>
        
      </ul>
    </nav>

    <main>
      
    </main>
  </div>
</template>


<script>

export default {
  
  data() {
    return {
      selectedTab: 'home',
    };
  },
  methods: {
    selectTab(tab) {
      this.selectedTab = tab;
    },
    
  },
  router: {
    base: '/',
  },
};
</script>



<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}

nav ul {
  list-style: none;
  display: flex;
  background-color: #333;
  padding: 10px;
  margin: 0;
}

nav li {
  margin: 10px;
  cursor: pointer;
  color: white;
}

.active {
  text-decoration: underline;
}

main {
  margin-top: 20px;
}

nav a {
  text-decoration: none;
  color: inherit;
}

</style>