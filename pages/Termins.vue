<template>
    <div>
      <div id="app" class="landing-page">
        <AppHeader />
      </div>
      <div v-if="reservationSuccess" class="success-modal">
            <p>Udana rezerwacja!</p>
            <p>Data i godzina: {{ selectedReservation.date }} {{ selectedReservation.time }}</p>
          </div>

      <div class="reservation-container">
        <ReservationForm
            v-if="showReservationForm"
            @submit="submitReservation"
            :reservation="selectedReservation"
          />
        <div>
          <div v-if="!isTerms" class="date-picker">
            <label for="datepicker">Wybierz datę:</label>
            <input lang="pl" type="date" id="datepicker" v-model="selectedDate" @input="filterByDate" />
          </div>
  
          <div v-if="filteredReservations.length === 0" class="no-reservations">
            <p>Nie ma dostępnych terminów do zarezerwowania w wybranym dniu.</p>
          </div>
  
          <div v-for="(reservation, index) in filteredReservations" :key="index" class="card">
            <div class="reservation-info">
              <p class="time">{{ reservation.time }}</p>
              <p class="cost">Cena: {{ reservation.cost }} zl</p>
            </div>
            <button @click="reserve(reservation)">Zarezerwować</button>
          </div>
  
          
          
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import AppHeader from '~/components/AppHeader.vue';
  import ReservationForm from './ReservationForm.vue';
  import { reservationsData } from './reservationsData.js';
  
  export default {
    props: {
      isTerms: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        selectedDate: null,
        reservations: reservationsData,
        filteredReservations: [],
        showReservationForm: false,
        selectedReservation: null,
        reservationSuccess: false,
      };
    },
    computed: {
      availableTerms() {
        return this.reservations.filter(term => term.date === this.selectedDate);
      },
    },
    methods: {
      filterByDate() {
        if (!this.isTerms) {
          this.filteredReservations = this.reservations.filter(reservation => {
            return reservation.date === this.selectedDate;
          });
  
          this.reservationSuccess = false;
        }
      },
      reserve(reservation) {
        this.selectedReservation = reservation;
        this.showReservationForm = true;
      },
      submitReservation(contactData) {
        console.log('Rezerwacja:', this.selectedReservation);
        console.log('Dane kontaktowe:', contactData);
        this.showReservationForm = false;
        this.reservationSuccess = true;
  
        const indexToRemove = this.reservations.findIndex(
          reservation =>
            reservation.date === this.selectedReservation.date &&
            reservation.time === this.selectedReservation.time
        );
        if (indexToRemove !== -1) {
          this.reservations.splice(indexToRemove, 1);
        }
      },
    },
    components: {
      AppHeader,
      ReservationForm,
    },
  };
  </script>
  
  <style scoped>
  .reservation-container {
    max-width: 600px;
    margin: auto;
  }
  
  .date-picker {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .no-reservations {
    text-align: center;
    margin-top: 20px;
  }
  
  .card {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .reservation-info {
    flex-grow: 1;
  }
  
  .time {
    font-size: 18px;
  }
  
  .cost {
    color: green;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
  }
  
  .success-modal {
    background-color: #4caf50;
    color: white;
    padding: 20px;
    margin-top: -20px;
    margin-bottom: 30px;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .success-modal p {
    margin: 10px 0;
  }
  
  
  .ReservationForm {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.9); 
    z-index: 100; 
    display: flex;
    justify-content: center;
    align-items: center;
  }
  </style>
  