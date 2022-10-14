
<template>

  <div class="row">
      <div class="col-12 mb-4">
         <progress-bar :porcentaje="porcentaje"/>
      </div>
  </div>



  <div class="row">
          <div class="col-12 col-md-4">
              <form @submit.prevent="registrarProyecto">
          <div class="mb-3">
              <label class="form-label">Proyecto</label>
              <input v-model.trim="proyecto" type="text" class="form-control" required />
          </div>

          <div class="mb-3">
              <label class="form-label">Actividad</label>
              <select v-model.trim="tipo" class="form-select" required>
                  <option disabled selected value="">Selecciona un tipo...</option>
                  <option >Aplicaciones Web con Vue.js</option>
                  <option >Backend Services con Node.js</option>
                  <option >App móvil con React Native</option>
              </select>
          </div>

          <div class="mb-3">
              <label for="exampleInputPassword1" class="form-check-label">Urgente</label>
              <input v-model="urgente" type="checkbox" class="form-check-input" />
          </div>


          <button type="submit" class="btn btn-primary">Guardar</button>

      </form>
      </div>
          <div class="col-12 col-md-8">
              <total-proyectos :numeroProyectos="numeroProyectos" :Proyectos="Proyectos" :CambiarEstado="CambiarEstado" :limpiarData="limpiarData" :eliminar="eliminar" />
          </div>
  </div>
  <hr>
</template> 


<script>
import { computed } from '@vue/reactivity';
import ProgressBar from './ProgressBar.vue';
import TotalProyectos from './TotalProyectos.vue';

  export default{
components: { ProgressBar, TotalProyectos },
      data:() => ({
          proyecto: "",
          tipo: "",
          urgente: false,
          proyectos: [],
      }),
      methods:{
          registrarProyecto(){
              const proyecto = {
                  proyecto: this.proyecto,
                  tipo: this.tipo,
                  urgente: this.urgente,
                  completado: false,
              };
              this.proyectos.push(proyecto);  
              
              this.saveData();

              this.proyecto = "";
              this.tipo = "";
              this.urgente = false;
          },
          CambiarEstado(proyecto, campo){
             
             proyecto[campo] = !proyecto[campo];
             this.saveData();
          },
          saveData(){
              localStorage.setItem("proyectos", JSON.stringify(this.proyectos));
          },
          Save(){
              localStorage.setItem("proyecto", JSON.stringify(this.proyecto, this.tipo, this.urgente ));
          },
      limpiarData(){
          this.proyectos = [];
          localStorage.clear();
      },
      eliminar: function(index) {
              // Borramos de la lista
           this.proyectos.splice(index, 1);
           this.saveData();
                              
          },

      },
      computed: {
          numeroProyectos(){
              return this.proyectos.length;
          },
          porcentaje (){
              let completados = 0;
              this.proyectos.map( proyecto => {
                  if(proyecto.completado)
                  completados++;
              })

              return (completados * 100) / this.numeroProyectos || 0;
          },
      },
      mounted(){
          this.proyectos = JSON.parse(localStorage.getItem("proyectos")) || [];
      },
  };
</script>

