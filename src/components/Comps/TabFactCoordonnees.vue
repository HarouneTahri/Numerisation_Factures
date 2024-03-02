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
            <BotonDetails @show-details="FactChoisi(item) "  />
          </td>
        </tr>
      </tbody>
    </table>
    </div>

  </div>
  
  <div>
   <AfficheDetailsFact ref="detailsModal" :items="detailsfacture" />
  </div>

  
</template>

<script>
import AfficheDetailsFact from './AfficheDetailsFact.vue';
import BotonDetails from './BotonDetails.vue'; 

export default {

  name: 'TabFactCoordonnees',

  components: {
    BotonDetails,
    AfficheDetailsFact 
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

    FactChoisi(item) {
      
      console.log('Détails de la facture:', item.InvoiceID);

      this.detailsfacture = this.items.find(facture => facture.InvoiceID === item.InvoiceID);

      console.log('Détails apres clique :', this.detailsfacture);

      this.AfficheDetailsFact.show("modal-details");
      //this.$refs.detailsModal.$bvModal.show();
      

    }
  }
}
</script>

<style scoped>

</style>
