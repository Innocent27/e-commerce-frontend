<template>
  <Navbar />
  <Login />
  <Footer />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import Login from "@/components/Login.vue";

export default {
  name: "App",
  components: { Login, Navbar, Footer },
};
</script>

<style></style>
