<template>
  <div class="card">
    <h3>{{ titulo }}</h3>
    <strong>{{ valor }}</strong>
  </div>
</template>

<script>
export default {
  props: {
    titulo: String,
    valor: Number,
  },
}
</script>

<style scoped>
.card {
  background: white;
  padding: 20px;
  border-radius: 10px;
  width: 180px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
</style>
