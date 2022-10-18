<script>
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
export default {
  data: () => ({
    nombre: "",
    edad: 0,
    correo: "",
  }),
  methods: {
    addUser() {
      console.warn(this.nombre, this.edad, this.correo);
    },
  },
  components: {
    Header,
    Formulario,
  }
};
</script>

<template>
  <div class="container text-center mt-4">
    <Header />
    <Formulario />
  </div>
</template>

<style scoped>

</style>
