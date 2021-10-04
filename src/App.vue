<template>


  <div id="app" class="overflow-hidden">

   <barra></barra>

  
       
       <div class="row ml-4">
          <div class="col-md-4"><convert/></div>
          <div class="col-md-4"><compare/></div>
       </div>

     
  </div>



</template>

<script>

import barra from './components/barra.vue'
import convert from './components/convert.vue'
import compare from './components/compare.vue'

export default {
  name: 'App',
  components: {
     barra,
     convert,
     compare
  }
}
</script>

