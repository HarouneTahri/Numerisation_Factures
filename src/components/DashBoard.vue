<template>


  <div >
    <RechercheBarre @search-query="getitemlibelle"/>
  </div>
  
  <div class="text-left">
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
      facturesdata: null
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

        return this.facturesdata.parents.filter(parent => {
        return parent.children.some(child => child.ItemLibelle === query);});

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