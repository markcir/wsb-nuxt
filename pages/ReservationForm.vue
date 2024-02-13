<template>
    <div>
      <div v-if="reservationSuccess" class="success-modal">
        <p>Dobra rezerwacja!</p>
        <p>Data i godzina: {{ selectedReservation.date }} {{ selectedReservation.time }}</p>
      </div>
  
      <h2 v-if="!reservationSuccess" class="text">Wprowadź swoje dane kontaktowe:</h2>
      <form v-if="!reservationSuccess" @submit.prevent="submitForm">
        <div>
          <label for="name">Imię</label>
          <input type="text" id="name" v-model="formData.name" required />
        </div>
        <div>
          <label for="phone">Nazwisko:</label>
          <input type="tel" id="secondNmae" v-model="formData.phone" required />
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="formData.email" required />
        </div>
        <button type="submit">Rezerwacja</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          name: '',
          phone: '',
          email: '',
        },
        reservationSuccess: false,
      };
    },
    methods: {
      submitForm() {
        if (this.validateForm()) {
          this.$emit('submit', this.formData);
          this.reservationSuccess = true; 
        } else {
          alert('Prosimy o wypełnienie wszystkich pól formularza.');
        }
      },
      validateForm() {
        return this.formData.name && this.formData.phone && this.formData.email;
      },
    },
  };
  </script>
  
  <style scoped>
 
  form {
    max-width: 300px;
    margin-left: 150px;
    margin-bottom: 50px;
  }
  .text {
    margin-left: 120px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
  }
  .success-modal {
    
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    z-index: 999;
    margin: 0px;
    padding: 0px;
  }
  
  .success-modal p {
    margin: 0px;
    
  }
  </style>