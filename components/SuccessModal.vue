<template>
    <b-modal v-model="showModal" title="Success" hide-footer>
      <p>Your request has been submitted successfully.</p>
      <b-button variant="primary" @click="closeModal">OK</b-button>
    </b-modal>
  </template>
  
  <script>
  export default {
    props: {
      showModal: Boolean
    },
    methods: {
      closeModal() {
        this.$emit("close-modal");
      }
    }
  };
  </script>