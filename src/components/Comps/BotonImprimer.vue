<template>
    <div>    
      <button @click="imprimer" >
        <img src="@/assets/imprimer.png" alt="Image du bouton" class="w-6 h-6">
      </button>
    </div>
  </template>
    
    <script>
      export default {
  
        name: 'BotonImprimer',
  
          methods: {
            imprimer() {
            this.$emit('imprimer'); 
          }
        }
      }
    </script>
    
    <style scoped>
  
  </style>