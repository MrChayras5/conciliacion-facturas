<template>
  <section>
    <h3>Seleccionar Factura PDF</h3>

    <input type="file" accept=".pdf" @change="seleccionarArchivo" />

    <div v-if="archivo">
      <h3>Archivo seleccionado</h3>

      <p><strong>Nombre:</strong> {{ archivo.name }}</p>
      <p><strong>Tamaño:</strong> {{ archivo.size }} bytes</p>
      <p><strong>Tipo:</strong> {{ archivo.type }}</p>

      <button @click="analizar">Analizar Factura</button>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      archivo: null,
    }
  },

  methods: {
    seleccionarArchivo(event) {
      this.archivo = event.target.files[0]
    },

    analizar() {
      this.$emit('analizar-factura', this.archivo)
    },
  },
}
</script>
