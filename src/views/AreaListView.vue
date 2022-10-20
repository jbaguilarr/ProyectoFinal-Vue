<template>
  <h1>Lista de areas</h1>
  <div class="container-sm">
      <table class="table">
        <thead class="table-dark">
            <tr>
                <th>Codigo</th>
                <th>Area</th>
                <th>Encargado</th>
                <th>Nro Funcionario</th>
                <th>Acciones</th>                
            </tr>
        </thead>
        <tbody>
            <tr v-for="(area,index) in ListaArea" :key="index">
                <td>{{area.id}}</td>
                <td>{{area.NombreArea}}</td>
                <td>{{area.NombreEncargado}}</td>
                <td>{{area.NroFuncionario}}</td>
                <td>
                    <button class="btn btn-primary m-2" @click="Accion('editar',area.id)">Editar</button>
                    <button class="btn btn-danger m-2" @click="Accion('eliminar',area.id)">Eliminar</button>
                </td>
            </tr>
        </tbody>
       </table>

  </div>
</template>

<script>
export default {
    name: 'AreaListView',
    data(){
             return {
                ListaArea : [],
             }
    },
    mounted() {
            this.getListArea();
    },
    methods: {
        getListArea () {
                // console.log(process.env);
                axios({
                    method: "get",
                    url: process.env.VUE_APP_RUTA_API+"/area"
                })
                    .then(response => {
                        this.ListaArea = response.data;
                        console.log(response);
                    })
                    .catch(e => console.log(e));
        },
        Accion (opcion, id)  {
            if (opcion === 'editar') {
                this.$router.push({ name: 'areasModificar', params: { id } });
            } else {
                if (confirm("Esta seguro de eliminar tarea")) {
                    axios({
                        method: "delete",
                        url: process.env.VUE_APP_RUTA_API+"/area/" + id
                    })
                        .then(response => {
                            this.getListArea();
                            console.log(response);
                        })
                        .catch(e => console.log(e));
                }
            }
        }
    }
}
</script>

<style>

</style>