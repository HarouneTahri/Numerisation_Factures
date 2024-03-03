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

  <br><br><br>
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
      allfacturedata : [],
      factrechercher : null
    };
  },

  props: {
    
  },

  mounted() {
    this.getAllFactData(); 
  },

  methods: {

     // recupirer a chaque fois value (char) entré en temps reel .. 
     //pour filtrer les facture qui contient produit rechercher

    getitemlibelle(query) {
      // supprimer les espaces debut et fin pour eviter les conflet ..

      query = query.trim();
      
      if (query ) { 
        // l'affectatio pour assurer en cas de suppression le filtrage .. 

        this.facturesdata = this.allfacturedata;
        this.facturesdata = this.facturesdata.filter(facture => {
          return facture.InvoiceItems.some(item => item.ItemLibelle.toLowerCase().includes(query.toLowerCase()));

        });
      }
       else{
        this.facturesdata = this.allfacturedata;
      }

    },


    // cette fonction pour retourner tout les donnees situées en l url ...
    async getAllFactData() {
      try {

        const response = await fetch('https://elhoussam.github.io/invoicesapi/db.json'); 
        if (!response.ok) {
          throw new Error('Erreur lors de la récupération des données');
        }
        
        const data = await response.json();
          this.allfacturedata = data;
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