<template>
    <div>    
      <button @click="imprimer" >
        <img src="@/assets/imprimericon.png" alt="Image du bouton" class="w-8 h-8">
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