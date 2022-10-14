<template>
  <div class="">
    <Header />
    <Formulario/>
    
    <hr/>

  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Formulario from "./components/formulario.vue"
export default{
  components: {
    Formulario,
    Header,
  }
}
  
</script>

<style scoped>
 

</style>