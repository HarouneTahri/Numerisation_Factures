<template>
  <div>    
    <button @click="showDetails" >
      <img src="@/assets/details.png" alt="Image du bouton" class="w-6 h-6">
    </button>
  </div>
</template>
  
  <script>
    export default {

      name: 'BotonDetails',

        methods: {
          showDetails() {
          this.$emit('show-details'); 
        }
      }
    }
  </script>
  
  <style scoped>

</style>