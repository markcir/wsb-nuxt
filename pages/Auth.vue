

<template>
    <div>
      <AppHeader />
      <div class="form-container">
        <h2>{{ formTitle }}</h2>
        <form @submit.prevent="submitForm">
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="username" required />
  
          
          <label v-if="isRegister" for="email">Email:</label>
          <input v-if="isRegister" type="email" id="email" v-model="email" required />
  
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="password" required />
  
          <button type="submit">{{ formButton }}</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import AppHeader from '~/components/AppHeader.vue';
  
  export default {
    data() {
      return {
        username: '',
        email: '',
        password: '',
      };
    },
    components: {
      AppHeader,
    },
    props: {
      isRegister: {
        type: Boolean,
        default: false,
      },
    },
    computed: {
      formTitle() {
        return this.isRegister ? 'Register' : 'Login';
      },
      formButton() {
        return this.isRegister ? 'Register' : 'Login';
      },
    },
    methods: {
      submitForm() {
        if (this.isRegister) {
          
          console.log('Register:', this.username, this.email, this.password);
        } else {
          
          console.log('Login:', this.username, this.password);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .form-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    text-align: center;
    background-color: #ecf9e8; 
    border: 1px solid #85af87; 
    border-radius: 5px; 
  }
  
  h2 {
    color: #4caf50;
  }
  
  label {
    color: #4caf50; 
  }
  
  input {
    padding: 8px;
    margin-bottom: 10px;
    width: 100%;
    box-sizing: border-box;
    border: 1px solid #4caf50; 
    border-radius: 5px; 
  }
  
  button {
    background-color: #4caf50; 
    color: #fff; 
    padding: 10px;
    border: none;
    border-radius: 5px; 
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049; 
  }
  
  </style>
  