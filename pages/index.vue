<script>
  import AppHeader from '~/components/AppHeader.vue';
  
  export default {
    data() {
      return {
        initialAnimation: true,
      };
    },
    methods: {
      redirectToLogoPage() {
        this.$router.push('/Termins');
      },
    },
    mounted() {
      
      setTimeout(() => {
        this.initialAnimation = false;
      }, 2000);
    },
    components: {
      AppHeader,
    },
  };
</script>

<template>
  <AppHeader />
  <div class="landing-page">
    <div class="logo-container">
      <img
        @click="redirectToLogoPage"
        class="logo"
        :class="{ 'animated': initialAnimation }"
        src="@/img/logo.png"
        alt="logo"
      />
    </div>
  </div>
</template>

<style scoped>
.landing-page {
  background-image: url('@/img/background1.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  margin-top: -20px;
}

.logo-container {
  position: relative;
}

.logo {
  width: 200px;
  height: 200px;
  cursor: pointer;
  position: relative;
  z-index: 1;
  transition: all 0.5s ease; 
}


.logo.animated {
  margin-top: -150px;
}


.logo-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 0px solid #4caf50; 
  border-radius: 0px; 
  opacity: 0;
  transition: opacity 0.8s ease;
}

.logo-container:hover::before {
  opacity: 1;
  top: -20px;
}

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
</style>
