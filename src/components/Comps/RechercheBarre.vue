<template>
   
   <div class="flex justify-center bg-gray-200 py-4">
   <input
      type="text"
      v-model="ItemLibelleChercher"
      placeholder="Rechercher un produit..."
      class="w-100 md:w-full max-w-md px-4 py-4 rounded-xl border border-gray-300 shadow-sm focus:outline-none focus:border-blue-500 text-gray-700"
      @keydown.enter="rechercher"
    />  
    </div>
  </template>
  
  <script>
  export default {
    name: 'RechercheBarre',
    
    
    data() {
      return {
        ItemLibelleChercher: ''
      };
    },

    methods: {
        rechercher() {
        this.$emit('search-query', this.ItemLibelleChercher); 
      }
    }
  }
  </script>
  
  <style scoped>


  </style>