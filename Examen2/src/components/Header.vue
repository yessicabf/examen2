<template>
  <div class="container mt-3">
   <div class="row">
   <div class="col-12 col-md-3"></div>
 <h1>FormularioExam_BFGY</h1>
 </div>
 <div class="col-12 col-md-6">
   <img :src="url" :alt="alt" width="100">
 </div>
 </div>
</template>


<script>
export default{
   data: () => ({
   url: "https://cdn.svgporn.com/logos/vue.svg",
   alt: "vue.js",
   nombre: "",
   edad: 0,
   correo: "",
 }),
};
 
</script>
