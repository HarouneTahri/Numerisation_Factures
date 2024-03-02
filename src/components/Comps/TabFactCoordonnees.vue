<template>
  <div>

    <div class="flex justify-center">
      <table class="mt-4 w-full max-w-3xl">
      <thead>
        <tr class="bg-gray-200">
          <th class="p-2">Facture ID</th>
          <th class="p-2">Facture Date</th>
          <th class="p-2">Client Nom</th>
          <th class="p-2">Fournisseur Nom</th>
          <th class="p-2">Montant TTC</th>
          <th class="p-2"></th>
          <th class="p-2"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="item.id" :class="index % 2 === 0 ? 'bg-gray-100' : 'bg-white'">
          <td class="p-2">{{ item.InvoiceID }}</td>
          <td class="p-2">{{ item.InvoiceDate }}</td>
          <td class="p-2">{{ item.ClientName }}</td>
          <td class="p-2">{{ item.SupplierName }}</td>
          <td class="p-2">{{ item.SupplierRC }}</td>
          <td class="p-2">
            <BotonDetails @show-details="FactDetailsChoisi(item) "  />
          </td>
          <td class="p-2">
            <BotonImprimer @imprimer="FactImprimerChoisi(item) "  />
          </td>
        </tr>
      </tbody>
    </table>
    </div>

  </div>
  

  
</template>

<script>
import BotonDetails from './BotonDetails.vue'; 
import BotonImprimer from './BotonImprimer.vue';
import VueHtml2Pdf from 'vue-html2pdf';

export default {

  name: 'TabFactCoordonnees',

  components: {
    BotonDetails,
    
    BotonImprimer 
  },

  
  data() {
    return {
      detailsfacture: [],
      showModal: false
    };
  },

  props: {
    items: {
      type: Array,
      required: true
    }
  },

  methods: {

    FactDetailsChoisi(item) {
      
      this.detailsfacture = this.items.find(facture => facture.InvoiceID === item.InvoiceID);
      console.log('Détails de facture choisi :', this.detailsfacture);
      
    },

    FactImprimerChoisi(item) {
      
      this.detailsfacture = this.items.find(facture => facture.InvoiceID === item.InvoiceID);
      console.log('facture a imprimer :', this.detailsfacture);
      

    },

    async generatePDF() {
      // Création d'un objet de configuration pour le PDF
      const options = {
        filename: 'facture.pdf', // Nom du fichier PDF
        image: { type: 'jpeg', quality: 0.98 }, // Type et qualité de l'image (optionnel)
        html2canvas: {}, // Options pour html2canvas (optionnel)
        jsPDF: {} // Options pour jsPDF (optionnel)
      };

      // Génération du PDF
      await VueHtml2Pdf.save('<h1>Facture</h1><p>Contenu de la facture ici...</p>', options);
    }

  }
}
</script>

<style scoped>

</style>
