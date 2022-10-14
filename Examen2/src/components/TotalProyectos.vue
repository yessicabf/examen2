<template>
    <div class="row">
    <div class="col-6 my-2">
        <h3>Total proyectos: {{ numeroProyectos }}</h3>
    </div>
    <div class="col-6 test-end">
       <button @click="limpiarData" class="btn btn-warning"> Limpia los proyectos</button> 
    </div>
</div>


<div class="table-responsive">
        <table class="table table-dark">
            <thead>
                <tr>
                    <th>#</th>
                    <th>proyecto</th>
                    <th>Tipo</th>
                    <th>Urgente</th>
                    <th>Completado</th>
                    <th>Borrar</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="(proyecto,index) in proyectos" :key="index">
                    <td>{{ index+1 }}</td>
                    <td>{{ proyecto.proyecto }}</td>
                    <td>{{proyecto.tipo }}</td>
                    <td @click="CambiarEstado(proyecto, 'urgente')" :class="proyecto.urgente ? 'bg-success' : 'bg-danger'">{{ proyecto.urgente ? "Si" : "No"}}</td>
                    <td @click="CambiarEstado(proyecto, 'completado')" :class="proyecto.completado ? 'bg-success' : 'bg-danger'">{{ proyecto.completado ? "Completo" : "Incompleto"}}</td>
                    
                   
                   <button @click="eliminar" class="btn btn-warning">Borrar</button>



                </tr>
            </tbody>
        </table>
    </div>
    <hr>
</template>

<script>
export default{
    props:['numeroProyectos', 'proyectos', 'CambiarEstado','limpiarData','eliminar'],
};
</script>