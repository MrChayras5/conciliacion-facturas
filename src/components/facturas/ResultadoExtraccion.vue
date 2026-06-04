<template>
  <div>
    <h3>Resultado de Extracción</h3>

    <p><strong>Folio:</strong> {{ resultadoExtraccion.folio }}</p>
    <p><strong>Proveedor:</strong> {{ resultadoExtraccion.proveedor }}</p>
    <p><strong>RFC:</strong> {{ resultadoExtraccion.rfc }}</p>
    <p><strong>UUID:</strong> {{ resultadoExtraccion.uuid }}</p>
    <p><strong>Total:</strong> {{ resultadoExtraccion.total }}</p>
  </div>
</template>

<script>
export default {
  props: {
    resultadoExtraccion: {
      type: Object,
      required: true,
    },
  },
}
</script>
