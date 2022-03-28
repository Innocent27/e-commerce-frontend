<template>
  <h1 class="fw-bold my-5">Product Details</h1>
  <MDBBtn
    color="black"
    onclick="history.back(-1)"
    class="link-button link-back-button"
  >
    Go Back
  </MDBBtn>
  <div class="container animate__animated animate__rubberBand">
    <div v-if="product" class="row d-flex justify-content-center">
      <div class="card-item text-dark border shadow-5-strong mt-5 card">
        <img :src="product.img_front" class="d-block img-thumbnail" alt="..." />
        <img
          :src="product.img_back"
          class="img-thumbnail img-top card-img"
          alt="..."
        />

        <div class="text-center">
          <p class="h5 names text-center">{{ product.title }}</p>
          <b class="category">{{ product.category }}</b>
          <div class=" ">
            <p class="text-center mt-3">{{ product.description }}</p>
            <p class="text-center mt-3">R{{ product.price }}</p>
          </div>
        </div>
        <div class="my-2">
          <MDBBtn
            color="black"
            aria-controls="exampleModal2"
            @click="exampleModal2 = true"
          >
            Update/Edit
          </MDBBtn>
          <router-link
            :to="{
              name: 'Dashboard',
            }"
          >
            <MDBBtn
              tag="a"
              href="#!"
              color="danger"
              @click.prevent="deleteProduct(product._id)"
              >Delete</MDBBtn
            >
          </router-link>
        </div>
      </div>
    </div>
    <div v-else>
      <p class="my-5">Loading product details...</p>
      <div class="fingerprint-spinner my-5">
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
        <div class="spinner-ring"></div>
      </div>
    </div>
  </div>
</template>

<script scoped>
import {
  MDBModal,
  MDBModalHeader,
  MDBModalTitle,
  MDBModalBody,
  MDBModalFooter,
  MDBBtn,
} from "mdb-vue-ui-kit";
import { ref } from "vue";
export default {
  props: ["id"],
  components: {
    MDBModal,
    MDBModalHeader,
    MDBModalTitle,
    MDBModalBody,
    MDBModalFooter,
    MDBBtn,
  },
  data() {
    return {
      product: null,
      title: "",
      category: "",
      description: "",
      img_front: "",
      img_back: "",
      price: "",
    };
  },
  mounted() {
    fetch("https://e-commerce-store-finalproject.herokuapp.com/products/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
      },
    })
      .then((response) => response.json())
      .then((json) => {
        this.product = json;
      })
      .catch((err) => {
        alert(console.log(err));
      });
  },

  setup() {
    const exampleModal2 = ref(false);
    return {
      exampleModal2,
    };
  },

  methods: {},
};
</script>

<style>
.card .img-top {
  display: none;
  position: absolute;
  top: 30.5px;
  left: 74px;
  z-index: 99;
}

.card:hover .img-top {
  display: inline;
  border-radius: 50%;
  height: 200px;
  margin: auto;
  width: 200px;
  object-fit: cover;
}

.d-block {
  border-radius: 50%;
  height: 200px;
  margin: auto;
  width: 200px;
  object-fit: cover;
}

.card-item {
  background-color: rgb(226, 226, 226);
  border-radius: 15px;
  min-height: 500px;
  max-width: 350px;
}
.category {
  color: rgb(255, 0, 0);
  font-size: x-large;
}
.names {
  font-size: xx-large;
}
.description {
  width: 700px !important;
}

.fingerprint-spinner,
.fingerprint-spinner * {
  box-sizing: border-box;
}

.fingerprint-spinner {
  height: 64px;
  width: 64px;
  padding: 2px;
  overflow: hidden;
  position: relative;
  display: inline-block;
}

.fingerprint-spinner .spinner-ring {
  position: absolute;
  border-radius: 50%;
  border: 2px solid transparent;
  border-top-color: #ff0000;
  animation: fingerprint-spinner-animation 1500ms
    cubic-bezier(0.68, -0.75, 0.265, 1.75) infinite forwards;
  margin: auto;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
}

.fingerprint-spinner .spinner-ring:nth-child(1) {
  height: calc(60px / 9 + 0 * 60px / 9);
  width: calc(60px / 9 + 0 * 60px / 9);
  animation-delay: calc(50ms * 1);
}

.fingerprint-spinner .spinner-ring:nth-child(2) {
  height: calc(60px / 9 + 1 * 60px / 9);
  width: calc(60px / 9 + 1 * 60px / 9);
  animation-delay: calc(50ms * 2);
}

.fingerprint-spinner .spinner-ring:nth-child(3) {
  height: calc(60px / 9 + 2 * 60px / 9);
  width: calc(60px / 9 + 2 * 60px / 9);
  animation-delay: calc(50ms * 3);
}

.fingerprint-spinner .spinner-ring:nth-child(4) {
  height: calc(60px / 9 + 3 * 60px / 9);
  width: calc(60px / 9 + 3 * 60px / 9);
  animation-delay: calc(50ms * 4);
}

.fingerprint-spinner .spinner-ring:nth-child(5) {
  height: calc(60px / 9 + 4 * 60px / 9);
  width: calc(60px / 9 + 4 * 60px / 9);
  animation-delay: calc(50ms * 5);
}

.fingerprint-spinner .spinner-ring:nth-child(6) {
  height: calc(60px / 9 + 5 * 60px / 9);
  width: calc(60px / 9 + 5 * 60px / 9);
  animation-delay: calc(50ms * 6);
}

.fingerprint-spinner .spinner-ring:nth-child(7) {
  height: calc(60px / 9 + 6 * 60px / 9);
  width: calc(60px / 9 + 6 * 60px / 9);
  animation-delay: calc(50ms * 7);
}

.fingerprint-spinner .spinner-ring:nth-child(8) {
  height: calc(60px / 9 + 7 * 60px / 9);
  width: calc(60px / 9 + 7 * 60px / 9);
  animation-delay: calc(50ms * 8);
}

.fingerprint-spinner .spinner-ring:nth-child(9) {
  height: calc(60px / 9 + 8 * 60px / 9);
  width: calc(60px / 9 + 8 * 60px / 9);
  animation-delay: calc(50ms * 9);
}

@keyframes fingerprint-spinner-animation {
  100% {
    transform: rotate(360deg);
  }
}
</style>
