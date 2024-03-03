<template>


  <div >
    <RechercheBarre @search-query="getitemlibelle"/>
  </div>
  <br>  
  <div class="text-center">
    <h1 class="text-3xl ml-4">Listes des factures  </h1>
  </div>

  <div >
    <TabFactCoordonnees :items="facturesdata"/>
  </div>

  

</template>

<script>


import RechercheBarre from './Comps/RechercheBarre.vue';
import TabFactCoordonnees from './Comps/TabFactCoordonnees.vue';

export default {

  name: 'DashBoard',

  components: {
    RechercheBarre,
    TabFactCoordonnees,
  },

  data() {
    return {
      facturesdata: [],
      factrechercher : null
    };
  },

  props: {
    
  },

  mounted() {
    this.getAllFactData(); 
  },

  methods: {

    getitemlibelle(query) {

        console.log('item libelle rechercher:', query);
       
        this.facturesdata = this.facturesdata.filter(facture => {
        return facture.InvoiceItems.some(item => item.ItemLibelle === query);

      });

      console.log('fonction contient item libelle :', this.facturesdata);

    },

    async getAllFactData() {
      try {

        const response = await fetch('https://elhoussam.github.io/invoicesapi/db.json'); 
        if (!response.ok) {
          throw new Error('Erreur lors de la récupération des données');
        }
        
        const data = await response.json();
          this.facturesdata = data;
      } catch (error) {
        console.error('Erreur :', error);
      }
    }



  }
}
</script>

<style>

</style>