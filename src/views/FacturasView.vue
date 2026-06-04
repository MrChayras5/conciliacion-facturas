<template>
  <section>
    <h1>Facturas</h1>

    <FacturaUpload @analizar-factura="analizarFactura" />

    <ResultadoExtraccion v-if="resultadoExtraccion" :resultadoExtraccion="resultadoExtraccion" />

    <ResultadoConciliacion
      v-if="resultadoConciliacion"
      :resultadoConciliacion="resultadoConciliacion"
    />
  </section>
</template>

<script>
import ResultadoConciliacion from '@/components/facturas/ResultadoConciliacion.vue'
import FacturaUpload from '../components/facturas/FacturaUpload.vue'
import ResultadoExtraccion from '../components/facturas/ResultadoExtraccion.vue'

export default {
  components: {
    FacturaUpload,
    ResultadoExtraccion,
    ResultadoConciliacion,
  },

  data() {
    return {
      resultadoExtraccion: null,
      resultadoConciliacion: null,
    }
  },

  methods: {
    analizarFactura(archivo) {
      console.log('Archivo recibido en FacturasView:', archivo)

      this.resultadoExtraccion = {
        folio: 'FAC-2026-0001',
        proveedor: 'Servicios Empresariales del Centro S.A. de C.V.',
        rfc: 'SEC980101AB1',
        uuid: 'A1B2C3D4-E5F6-7890-ABCD-1234567890EF',
        total: 17400,
      }

      this.conciliarFactura()
    },

    conciliarFactura() {
      const registroBD = {
        folio: 'FAC-2026-0001',
        proveedor: 'Servicios Empresariales del Centro S.A. de C.V.',
        total: 17200,
      }

      const diferencias = []

      if (this.resultadoExtraccion.folio !== registroBD.folio) {
        diferencias.push({
          campo: 'Folio',
          pdf: this.resultadoExtraccion.folio,
          bd: registroBD.folio,
        })
      }

      if (this.resultadoExtraccion.total !== registroBD.total) {
        diferencias.push({
          campo: 'Total',
          pdf: this.resultadoExtraccion.total,
          bd: registroBD.total,
        })
      }

      this.resultadoConciliacion = {
        estatus: diferencias.length === 0 ? 'CONCILIADO' : 'CONCILIADO CON DIFERENCIA',
        diferencias: diferencias,
      }
    },
  },
}
</script>
