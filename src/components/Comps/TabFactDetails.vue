<template>
    <div class="flex justify-center">
      <table class="mt-4 w-full max-w-3xl">
       
        <thead >
        
          <tr class="bg-gray-200">
        
            <th class="p-2">Item Libelle</th>
            <th class="p-2">Unité d Item</th>
            <th class="p-2">Quantité d item</th>
            <th class="p-2">Prix d item</th>
            <th class="p-2">Taxe d item</th>
            <th class="p-2">Montant d item TTC</th>

          </tr>
        </thead>
       
        <tbody>
          <tr v-for="(item, index) in items"
            :key="item.id"
            :class="index % 2 === 0 ? 'bg-gray-100' : 'bg-white'">
            
            <td class="p-2">{{ item.ItemLibelle }}</td>
            <td class="p-2">{{ item.ItemUnit }}</td>
            <td class="p-2">{{ Item.Quantity }}</td>
            <td class="p-2">{{ item.ItemPrice }}</td>
            <td class="p-2">{{ item.ItemTax }}</td>
            <td class="p-2">{{item.ItemPrice * Item.Quantity + item.ItemTax * Item.Quantity  }}</td>

          </tr>
        </tbody>
     
    </table>
    </div>
  </template>
  
  <script>
  export default {
    
    name: 'TabFactDetails',
    
    props: {
      items: {
        type: Array,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  

  </style>