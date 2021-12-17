<template>
  <main>
    <section class="banner">
      <h1 class="banner__title">Make your burger</h1>
    </section>
    <burgerForm />
  </main>
</template>

<script>
  import burgerForm from '../components/burgerForm.vue'
export default {
  name: 'Home',
  components: {
    burgerForm
  }
}
</script>

<style scoped>
.banner {
  width: 100%;
  height: 80vh;
  background-image: url(../assets/burger.jpg);
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  z-index: -1;
  display: flex;
  align-items: center;
}
.banner__title {
  color: white;
  background: rgba(51, 51, 51, 0.781);
  font-size: 2.5em;
  padding: .3em .5em .3em 1em;
}
@media only screen and (min-width: 768px) {
  .banner__title {
    font-size: 3.5em;
    padding: .3em .5em .3em 2em;
  }
}
</style>
