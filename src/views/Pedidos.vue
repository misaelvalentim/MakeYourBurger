<template>
  <section class="dashboard">
    <h1 class="dashboard__title">Gerenciar pedidos</h1>
    <dashboard/>
  </section>
</template>
<script>
  import dashboard from '../components/dashboard.vue'
export default {
  name: 'Pedidos',
  components: {
    dashboard
  }
}
</script>
<style scoped>
  .dashboard {
    min-height: 70vh;
  }
  .dashboard__title{
    text-align: center;
  }
</style>
