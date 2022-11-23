<template>
  <div>
    <router-link to="/addConsumo">Agregar Consumo</router-link>
  </div>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Fecha</th>
      <th scope="col">Usuario</th>
      <th scope="col">Consumo</th>
      <th scope="col">Total a pagar</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(consumo, index) in consumos">
      <th scope="row">{{index+1}}</th>
      <td>{{consumo.fecha_lectura}}</td>
      <td>{{consumo.id_usuario}}</td>
      <td>{{consumo.cantidad_consumo}}</td>
      <td>{{consumo.total}}</td>
      <td><app-acciones @onAccion="irA($event, consumo.id)"></app-acciones></td>
    </tr>
    </tbody>
  </table>
</template>

<script>
import AppAcciones from '@/components/AppAcciones.vue';


export default {
  name: 'appTable',
  data() {
    return {

      consumos: null,
      propietrios:null,
      loading: true,
      errored: false
    }
  },
  methods: {
    irA(opcion, consumo_id) {
      if (opcion === 'editar') {
        this.$router.push({ name: 'editarConsumoView', params: { id: consumo_id } });
      } else {
        if (confirm("Esta seguro de eliminar el consumo")) {
          axios({
            method: "delete",
            url: "http://localhost:4444/consumos/" + consumo_id
            // url: process.env.VUE_APP_RUTA_API+"/consumos/" + consumo_id
          })
              .then(response => {
                this.getConsumos();
                console.log(response);
              })
              .catch(e => console.log(e));
        }
      }
    },

    getConsumos() {
      axios({
        method: "get", 
        url: "http://localhost:4444/consumos"
        // url: process.env.VUE_APP_RUTA_API+"/consumos"
      })
          .then(response => {
            this.consumos = response.data;
            console.log(response);
          })
          .catch(e => console.log(e));
    },
    getConsumoId(idConsum) {
            axios({
                method: "get",
                url: "http://localhost:4444/propietarios/"+idConsum
            })
                .then(response => {
                    this.propietarios = response.data;
                    console.log("esto es el propietario"+propietarios.nombre);
                })
                .catch(e => console.log(e));
        },
  },
  computed: {},
  mounted() {
    axios.get('http://localhost:4444/consumos')
        .then(response => {
          this.consumos = response.data
        })
        .catch(error => {
          console.log(error)
          this.errored = true
        })
        .finally(() => this.loading = false)
  },
  components: {
    AppAcciones
  }
}
</script>

<style>

</style>