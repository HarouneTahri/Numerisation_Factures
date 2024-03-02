<template>

    <div class="modal-overlay fixed inset-0 bg-black opacity-50 z-50"></div>
    <div class="modal-container fixed inset-0 flex items-center justify-center z-50">
      <div class="modal-content bg-white p-8">
        <h2 class="text-xl mb-4">Détails</h2>

        <TabFactDetails :items="items"/>
       
        <TabComponent :data="tableData" />
        <button @click="closeModal" class="mt-4 px-4 py-2 bg-blue-500 text-white rounded">Fermer</button>
      </div>
    </div>

  </template>
  
  <script>
import TabFactDetails from './TabFactDetails.vue';

  export default {

    name: 'AfficheDetailsFact',

    components : TabFactDetails , 
   
    props: {
      items: {
        type: Array,
        required: true
      }
    },

    methods: {
      closeModal() {
        this.$emit('close-modal');
      }
    }
  }
  </script>
  
  <style scoped>
  /* Styles spécifiques au composant modal */
  </style>