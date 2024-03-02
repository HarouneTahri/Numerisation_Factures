<template>
    <div>
      <table>
       
        <thead>
          <tr>
           
            <th>Item Libelle</th>
            <th>Unité d Item</th>
            <th>Quantité d item</th>
            <th>Prix d item</th>
            <th>Taxe d item</th>
            <th>Montant d item TTC</th>

          </tr>
        </thead>
       
        <tbody>
          <tr v-for="item in items" :key="item.id">
            
            <td>{{ item.ItemLibelle }}</td>
            <td>{{ item.ItemUnit }}</td>
            <td>{{ Item.Quantity }}</td>
            <td>{{ item.ItemPrice }}</td>
            <td>{{ item.ItemTax }}</td>
            <td>{{ Item.Quantity * item.ItemPrice + Item.Quantity * item.ItemTax }}</td>

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