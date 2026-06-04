<template>
  <section>
    <h1>DashBoard</h1>
    <p>Resumen general del proceso de conciliacion</p>
    <div class="card">
      <h3>
        Bienvenido: <strong>{{ nombreUsuario }}</strong>
      </h3>
    </div>

    <div class="cards">
      <DashboardCard titulo="Facturas Cargadas" :valor="facturasCargadas" />

      <DashboardCard titulo="Conciliadas" :valor="conciliadas" />

      <DashboardCard titulo="Con Diferencias" :valor="conDiferencias" />

      <DashboardCard titulo="No Conciliadas" :valor="noConciliadas" />
      <DashboardCard titulo="PruebaCrd" :valor="prueba" />
    </div>

    <button @click="sumarFactura">Agregar Factura</button>

    <FacturaTabla :facturas="facturasFiltradas" @eliminar-factura="eliminarFactura" />

    <p v-if="facturasFiltradas.length === 0">No se encontraron facturas con esa busqueda.</p>

    <h2>Busqueda de Factura</h2>

    <input type="text" v-model="busqueda" />
    <p>Estas buscando: {{ busqueda }}</p>

    <FacturaForm @guardar-factura="agregarFactura" />
  </section>
</template>

<script>
import DashboardCard from '../components/dashboard/DashboardCard.vue'
import FacturaForm from '../components/facturas/FacturaForm.vue'
import FacturaTabla from '../components/facturas/FacturaTabla.vue'

export default {
  components: {
    DashboardCard,
    FacturaForm,
    FacturaTabla,
  },

  data() {
    return {
      nombreUsuario: 'Diego',
      facturasCargadas: 25,
      conciliadas: 20,
      conDiferencias: 3,
      noConciliadas: 2,
      prueba: 2,
      facturas: [
        {
          id: 1,
          folio: 'FAC-001',
          proveedor: 'Telmex',
          monto: 15000,
        },
        {
          id: 2,
          folio: 'FAC-002',
          proveedor: 'Axtel',
          monto: 12000,
        },
        {
          id: 3,
          folio: 'FAC-003',
          proveedor: 'Izzi',
          monto: 18000,
        },
      ],
      busqueda: '',
    }
  },

  computed: {
    facturasFiltradas() {
      return this.facturas.filter((factura) => {
        const texto = this.busqueda.toLowerCase()

        return (
          factura.folio.toLowerCase().includes(texto) ||
          factura.proveedor.toLowerCase().includes(texto)
        )
      })
    },
  },

  methods: {
    sumarFactura() {
      this.facturasCargadas++
    },
    agregarFactura(factura) {
      const nuevaFactura = {
        id: this.facturas.length + 1,
        folio: factura.folio,
        proveedor: factura.proveedor,
        monto: factura.monto,
        estatus: 'Pendiente',
      }

      this.facturas.push(nuevaFactura)
      this.facturasCargadas++
    },
    eliminarFactura(id) {
      this.facturas = this.facturas.filter((factura) => factura.id !== id)
    },
  },
}
</script>

<style scoped>
.cards {
  display: flex;
  gap: 16px;
  margin-top: 20px;
}

.card {
  background: white;
  padding: 20px;
  border-radius: 10px;
  width: 180px;
}

.formulario-factura {
  display: flex;
  gap: 16px;
  margin-top: 10px;
  margin-bottom: 20px;
}

.campo {
  display: flex;
  flex-direction: column;
}

.campo label {
  font-weight: bold;
  margin-bottom: 6px;
}

.campo input {
  padding: 8px;
  border: 1px solid #aaa;
  border-radius: 6px;
}
</style>
