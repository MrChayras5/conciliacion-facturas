<template>
  <div class="formulario">
    <h2>Registrar Factura</h2>

    <input type="text" v-model="folio" placeholder="Folio" />

    <input type="text" v-model="proveedor" placeholder="Proveedor" />

    <input type="number" v-model="monto" placeholder="Monto" />
  </div>
  <button @click="guardar">Guardar Factura</button>
</template>

<script>
export default {
  data() {
    return {
      folio: '',
      proveedor: '',
      monto: '',
    }
  },

  methods: {
    guardar() {
      const factura = {
        folio: this.folio,
        proveedor: this.proveedor,
        monto: this.monto,
      }

      this.$emit('guardar-factura', factura)

      this.folio = ''
      this.proveedor = ''
      this.monto = ''
    },
  },
}
</script>
