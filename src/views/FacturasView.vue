<template>
  <section>
    <H1>Facturas</H1>
    <h3>Selecciona el archivo PDF</h3>

    <input type="file" accept="pdf" @change="seleccionarArchivo" />

    <div v-if="archivo">
      <h3>Archivo seleccionado</h3>
      <p><strong>Nombre: </strong>{{ archivo.name }}</p>
      <p><strong>Tamaño: </strong>{{ archivo.size }}</p>
      <p><strong>Tipo: </strong>{{ archivo.type }}</p>
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
      this.archivo = event.target.file[0]
      console.log(this.archivo)
    },
  },
}
</script>
