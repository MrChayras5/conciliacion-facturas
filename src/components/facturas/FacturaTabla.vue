<template>
  <h2>Tabla de facturas</h2>
  <table border="5">
    <thead>
      <tr>
        <th>ID</th>
        <th>Folio</th>
        <th>Proveedor</th>
        <th>Monto</th>
        <th>Estatus</th>
        <th>Acciones</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="factura in facturas" :key="factura.id">
        <td>{{ factura.id }}</td>
        <td>{{ factura.folio }}</td>
        <td>{{ factura.proveedor }}</td>
        <td>{{ factura.monto }}</td>
        <td>{{ factura.estatus }}</td>
        <td><button @click="eliminar(factura.id)">Eliminar</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    facturas: {
      type: Array,
      required: true,
    },
  },

  methods: {
    eliminar(id) {
      this.$emit('eliminar-factura', id)
    },
  },
}
</script>
