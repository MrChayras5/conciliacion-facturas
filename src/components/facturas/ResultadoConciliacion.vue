<template>
  <div>
    <h3>Resultado de Conciliación</h3>

    <p>
      <strong>Estatus:</strong>
      {{ resultadoConciliacion.estatus }}
    </p>

    <table v-if="resultadoConciliacion.diferencias.length > 0" border="1">
      <thead>
        <tr>
          <th>Campo</th>
          <th>PDF</th>
          <th>BD</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="dif in resultadoConciliacion.diferencias" :key="dif.campo">
          <td>{{ dif.campo }}</td>
          <td>{{ dif.pdf }}</td>
          <td>{{ dif.bd }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    resultadoConciliacion: {
      type: Object,
      required: true,
    },
  },
}
</script>
