<template>
  <section>
    <H1>Facturas</H1>
    <h3>Selecciona el archivo PDF</h3>

    <input type="file" accept=".pdf" @change="seleccionarArchivo" />

    <div v-if="archivo">
      <h3>Archivo seleccionado</h3>
      <p><strong>Nombre: </strong>{{ archivo.name }}</p>
      <p><strong>Tamaño: </strong>{{ archivo.size }}</p>
      <p><strong>Tipo: </strong>{{ archivo.type }}</p>
    </div>

    <button v-if="archivo" @click="analizarFactura">Analizar factura</button>

    <div v-if="resultadoExtraccion">
      <h3>Resultado de Extracción</h3>

      <p><strong>Folio:</strong> {{ resultadoExtraccion.folio }}</p>
      <p><strong>Proveedor:</strong> {{ resultadoExtraccion.proveedor }}</p>
      <p><strong>RFC:</strong> {{ resultadoExtraccion.rfc }}</p>
      <p><strong>UUID:</strong> {{ resultadoExtraccion.uuid }}</p>
      <p><strong>Total:</strong> {{ resultadoExtraccion.total }}</p>
    </div>

    <div v-if="resultadoConciliacion">
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
  </section>
</template>

<script>
export default {
  data() {
    return {
      archivo: null,
      resultadoExtraccion: null,
      resultadoConciliacion: null,
    }
  },

  methods: {
    seleccionarArchivo(event) {
      this.archivo = event.target.files[0]
      console.log(this.archivo)
    },
    analizarFactura() {
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
