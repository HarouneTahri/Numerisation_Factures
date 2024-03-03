<template>

  <b-modal ref="modal" title="Tableau de données">
      <div class="d-block">
    
        <TabFactDetails :items="donneesfact"/>
          
      </div>
      
  </b-modal>

  </template>
  
  <script>
import TabFactDetails from './TabFactDetails.vue';
  export default {

    name: 'AfficheDetailsFact',

    components :{
         TabFactDetails , 
         
      },
             
    data() {
     return {
       donneesfact: []
     };
    },
  methods: {
    openModal(data) {
      this.donneesfact = data;
      this.$refs.modal.show();
    }
   }
  };
  </script>
  
  <style scoped>
  /* Styles spécifiques au composant modal */
  </style>