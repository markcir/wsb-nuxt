
<template>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <ReservationForm @submit="submitReservation" :reservation="selectedReservation" />
      </div>
    </div>
  </template>
  
  <script>
  import ReservationForm from './ReservationForm.vue';
  
  export default {
    props: {
      showModal: Boolean,
      selectedReservation: Object,
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },
      submitReservation(contactData) {
        console.log('Rezerwacja:', this.selectedReservation);
        console.log('Dane kontaktowe:', contactData);
        this.closeModal();
      },
    },
    components: {
      ReservationForm,
    },
  };
  </script>