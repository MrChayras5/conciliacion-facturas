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

    <h2>Facturas Procesadas</h2>

    <table border="5">
      <thead>
        <tr>
          <th>ID</th>
          <th>Folio</th>
          <th>Proveedor</th>
          <th>Monto</th>
          <th>Estatus</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="factura in facturasFiltradas" :key="factura.id">
          <td>{{ factura.id }}</td>
          <td>{{ factura.folio }}</td>
          <td>{{ factura.proveedor }}</td>
          <td>{{ factura.monto }}</td>
          <td>{{ factura.estatus }}</td>
        </tr>
      </tbody>
    </table>

    <p v-if="facturasFiltradas.length === 0">No se encontraron facturas con esa busqueda.</p>

    <h2>Busqueda de Factura</h2>

    <input type="text" v-model="busqueda" />
    <p>Estas buscando: {{ busqueda }}</p>

    <h2>Registrar Factura</h2>

    <div class="formulario-factura">
      <div class="campo">
        <label>Folio</label>
        <input type="text" v-model="folio" placeholder="Ejemplo: FAC-004" />
      </div>

      <div class="campo">
        <label>Proveedor</label>
        <input type="text" v-model="proveedor" placeholder="Ejemplo: Izzi" />
      </div>

      <div class="campo">
        <label>Monto</label>
        <input type="number" v-model="monto" placeholder="Ejemplo: 15000" />
      </div>
    </div>

    <h2>Vista previa</h2>
    <p>Folio: {{ folio }}</p>
    <p>Proveedor: {{ proveedor }}</p>
    <p>Monto: {{ monto }}</p>

    <button @click="agregarFactura">Guardar Factura</button>
  </section>
</template>

<script>
import DashboardCard from '../components/DashboardCard.vue'

export default {
  components: {
    DashboardCard,
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
      folio: '',
      proveedor: '',
      monto: '',
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
    agregarFactura() {
      const nuevaFactura = {
        id: this.facturas.length + 1,
        folio: this.folio,
        proveedor: this.proveedor,
        monto: this.monto,
        estatus: 'Pendiente',
      }

      this.facturas.push(nuevaFactura)

      this.facturasCargadas++

      this.folio = ''
      this.proveedor = ''
      this.monto = ''
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
