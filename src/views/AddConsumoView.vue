<template>
  <div class="container">
    <div class="abs-center">
      <form action="" @submit.prevent="guardar()">
        <!-- <div class="mb-3">
          <label class="form-label">Avatar</label>
          <input type="text" v-model="propietario.avatar" class="form-control">
        </div> -->
        <h1>Agregar Usuario</h1>
        <div class="mb-3">
          <label class="form-label">Fecha</label>
          <input type="text"  v-model="propietario.nombres" class="form-control">
        </div>
        <div class="mb-3">
          <label class="form-label">Usuario</label>
          <input type="text" v-model="propietario.paterno" class="form-control">
        </div>
        <div class="mb-3">
          <label class="form-label">Consumo</label>
          <input type="text" v-model="propietario.materno" class="form-control">
        </div>
        <div class="mb-3">
          <label class="form-label">Total a pagar</label>
          <input type="text" v-model="propietario.celular" class="form-control">
        </div>

        <button type="submit" class="btn btn-primary m-2">Guardar</button>
        <!-- <button class="btn btn-light m-2">Cancelar</button> -->
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'agregarConsumo',
  data() {
    return {
      consumo: {
        id_usuario: 1,
        cantidad_consumo: null,
        fecha_lectura: null,
        total: null,
        id:null,
      }
    }
  },
  methods: {
    getConsumo() {
      axios({
        method: "get", 
        url: "http://localhost:4444/consumos/" 
        // url: process.env.VUE_APP_RUTA_API + "/propietarios/" + this.$route.params.id
      })
          .then(response => {
            this.consumo = response.data;
            console.log(response);
          })
          .catch(e => console.log(e));
    },
    guardar() {
      axios({
        method: "post",
        url: "http://localhost:4444/consumos/",
        // url: process.env.VUE_APP_RUTA_API + "/propietarios/" + this.$route.params.id,
        data: this.consumo
      })
          .then(response => {
            this.$store.state.mensaje = {
              texto: "El consumo se agrego exitosamente",
              tipo: "exito"
            };
            this.$store.dispatch('addMensajeAction');
            this.$router.push({name: 'consumos'});
          })
          .catch(e => console.log(e));
    }
  },
  computed: {},
  mounted() {
    this.getConsumo()
  },
  components: {}
}
</script>

<style scoped>
form {
  max-width: 400px;
}
</style>