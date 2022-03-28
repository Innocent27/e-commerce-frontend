<template>
  <Navbar />
  <Register />
  <Footer />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import Register from "@/components/Register.vue";

export default {
  name: "App",
  components: { Register, Navbar, Footer },
};
</script>

<style></style>
