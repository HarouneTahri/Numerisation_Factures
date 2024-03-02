<template>

  <b-modal id="modal-details" hide-header>
      <div class="d-block">
    
        <TabFactDetails :items="items"/>
          
      </div>
      <div>
        <BotonImprimer/>
      </div>
    </b-modal>

  </template>
  
  <script>
import TabFactDetails from './TabFactDetails.vue';
import BotonImprimer from './BotonImprimer.vue';
  export default {

    name: 'AfficheDetailsFact',

    components :{
         TabFactDetails , 
         BotonImprimer
      },
             
    props: {
      items: {
        type: Array,
        required: true
      }
    },

    methods: {
     
    }
  }
  </script>
  
  <style scoped>
  /* Styles spécifiques au composant modal */
  </style>