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
          <tr
            v-for="(item, index) in items"
            :key="item.id"
            :class="index % 2 === 0 ? 'bg-gray-100' : 'bg-white'"
          >
            <td class="p-2">{{ item.InvoiceID }}</td>
            <td class="p-2">{{ item.InvoiceDate }}</td>
            <td class="p-2">{{ item.ClientName }}</td>
            <td class="p-2">{{ item.SupplierName }}</td>
            <td class="p-2">{{ item.SupplierRC }}</td>
            <td class="p-2">
              <BotonDetails @click="selectedItem = item" />
            </td>
            <td class="p-2">
              <BotonImprimer @imprimer="FactImprimerChoisi(item)" />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <DetailsFact
      v-if="selectedItem"
      :item="selectedItem"
      :close="hideDetails"
    />
  </div>
</template>

<script>
import BotonDetails from "./BotonDetails.vue";
import BotonImprimer from "./BotonImprimer.vue";
import html2pdf from "html2pdf.js";
import DetailsFact from "./DetailsFact.vue";

export default {
  name: "TabFactCoordonnees",

  components: {
    BotonDetails,
    BotonImprimer,
    DetailsFact,
  },

  data() {
    return {
      detailsfacture: [],
      dialogVisible: false,
      selectedItem: null,
    };
  },

  props: {
    items: {
      type: Array,
      required: true,
    },
  },

  methods: {
    hideDetails() {
      this.selectedItem = null;
    },

    // fonction se declanche apres le clique sur le botton de detaille de facture ..
    // et puis recuperer les donnees de la facture selectionner ..

    FactDetailsChoisi(item) {
      this.detailsfacture = this.items.find(
        (facture) => facture.InvoiceID === item.InvoiceID
      );
    },
    // fonction se declanche apres le clique sur le botton de imprimer facture ..
    // et puis recuperer les donnees de la facture selectionner..
    // calculer le total et total de tva et total a payer et l'envoyer a la forme htmlgeneratePDF

    FactImprimerChoisi(item) {
      this.detailsfacture = this.items.find(
        (facture) => facture.InvoiceID === item.InvoiceID
      );
      console.log("facture a imprimer :", this.detailsfacture);

      let total = 0;
      let totaltva = 0;

      this.detailsfacture.InvoiceItems.forEach((item) => {
        total += item.ItemQuantity * item.ItemPrice;
        totaltva += item.ItemQuantity * item.ItemTax;
      });

      this.generatePDF(this.detailsfacture, total, totaltva, total + totaltva);
    },

    // fonction qui contient le forme de la facture html et apres elle sera convertir a PDF..

    async generatePDF(donneesfacture, total, totaltva, totalprix) {
      const content = `
      <div style="margin-top: 50px; margin-left: 80px; margin-right: 80px;"> 

      <h1  style="font-size: 24px; text-align: center; font-weight: bold;">Facture N : ${
        donneesfacture.InvoiceID
      }</h1><br>

      <p style="position: absolute;  left: 60%;">Date de facture : ${
        donneesfacture.InvoiceDate
      }</p><br>
      
      
        <div style="margin-top: 12%; margin-left: 5%; margin-right: 60%;" >
          <p>Fournisseur</p>
          <hr style="width: 100%; height: 2px; background-color: black; border: none; margin: 10px auto;">
          <p style="font-size: 20px; font-weight: bold;">${
            donneesfacture.SupplierName
          }</p>
          <p>${donneesfacture.SupplierPhone}</p>
          <p>${donneesfacture.SupplierAddress}</p>
        </div>
      
        <div  style="position: absolute; top: 230px; left: 500px;">
          <p>Client</p>
          <hr style="width: 100%; height: 2px; background-color: black; border: none; margin: 10px auto;">
          <p style="font-size: 20px;  font-weight: bold;">${
            donneesfacture.ClientName
          }</p>
          <p>${donneesfacture.ClientPhone}</p>
          <p>${donneesfacture.SupplierAddress}</p>
        </div>
      <br><br>
      <br><br>
        <table style="width: 600px; margin: 0 auto;   " >
        <thead>
          <tr class="bg-yellow-200">
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 40px;">Num</th>
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 250px;">LIBELLE</th>
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 80px;">Quantite</th>
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 80px;">Prix</th>
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 80px;">HT</th>
            <th style="border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px;">TTC</th>
          </tr>
        </thead>
        <tbody>
          ${donneesfacture.InvoiceItems.map(
            (item, index) => `
          <tr key="${index}" >
            <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemID
            }</td>
            <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemLibelle
            }</td>
            <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemQuantity
            }</td>
            <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemPrice
            }</td>
            <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemQuantity * item.ItemPrice
            }</td>
            <td style="text-align: center; border: 1px solid black;vertical-align: middle;line-height: 50px;">${
              item.ItemQuantity * item.ItemPrice -
              item.ItemTax * item.ItemQuantity
            }</td>
          </tr>
        `
          ).join("")}
      </tbody>
     </table>

     <br>
    
     <table style=" margin-left: 50%; width: 300px;   ">
      <tbody>
        <tr>
         <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px; ">TOTAL</td>
         <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px; height: 20px;">${total}</td>
        </tr>
        <tr>
         <td style=" text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px; ">TVA</td>
         <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px; height: 20px;">${totaltva}</td>
        </tr>
        <tr>
         <td style="font-weight: bold;text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px; ">TOTAL TTC</td>
         <td style="text-align: center;border: 1px solid black;vertical-align: middle;line-height: 50px;width: 200px;height: 20px;">${totalprix}</td>
        </tr>
      </tbody>
    </table>

    <div style=" margin-left: 70%; margin-top: 30%;">
    <p >LA SIGNATURE</p><br>
    </div>

    </div>
  </div>
`;

      // les proprietés de pdf qu' on veut apres la convertion..
      const options = {
        filename: "facture.pdf",
        image: { type: "jpeg", quality: 1.0 },
        jsPDF: { format: "a4" },
      };
      // la convertion vers le PDF
      html2pdf().from(content).set(options).save();
    },
  },
};
</script>

<style scoped></style>