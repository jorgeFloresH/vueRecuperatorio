<template>
  <div>
    <h1>{{ titulo }}</h1>
  </div>
  <consumos-table title="Lista de Consumos"></consumos-table>
</template>

<script>
import ConsumosTable from '@/components/ConsumoTable.vue';

export default {
  name: 'consumosView',
  data() {
    return {
      titulo: "Consumos"
    }
  },
  methods: {},
  mounted() {

  },
  components: {
    ConsumosTable
  }
}
</script>