<template>
  <Navbar />
  <!-- Button trigger modal -->
  <MDBModal
    id="exampleModal2"
    tabindex="-1"
    labelledby="exampleModalLabel2"
    v-model="exampleModal2"
  >
    <MDBModalHeader>
      <MDBModalTitle id="exampleModalLabel2"> Update Product </MDBModalTitle>
    </MDBModalHeader>
    <MDBModalBody>
      <div class="mb-3">
        <label for="addTitle" class="form-label">Title</label>
        <input
          class="form-control"
          type="text"
          name="addTitle"
          id="addTitle"
          v-model="title"
        />
      </div>
      <div class="mb-3">
        <label for="" class="form-label">Category</label>
        <select
          class="form-select"
          name="addCategory"
          id="addCategory"
          v-model="category"
        >
          <option value="Samsung">Samsung</option>
          <option value="Huawei">Huawei</option>
          <option value="Apple">Apple</option>
        </select>
      </div>
      <div class="mb-3">
        <label for="addPrice" class="form-label">Price</label>
        <input
          class="form-control"
          type="text"
          name="addPrice"
          id="addPrice"
          v-model="price"
        />
      </div>
      <div class="mb-3">
        <label for="addImg" class="form-label">Image Front URL</label>
        <input
          class="form-control"
          type="text"
          name="addImg"
          id="addImg"
          v-model="img_front"
        />
      </div>
      <div class="mb-3">
        <label for="addImg" class="form-label">Image Back URL</label>
        <input
          class="form-control"
          type="text"
          name="addImg"
          id="addImg"
          v-model="img_back"
        />
      </div>
      <div class="mb-3">
        <label for="addDescription" class="form-label">Description</label>
        <input
          class="form-control"
          type="text"
          name="addDescription"
          id="addDescription"
          v-model="description"
        />
      </div>
    </MDBModalBody>
    <MDBModalFooter>
      <MDBBtn color="secondary" @click="exampleModal2 = false">Close</MDBBtn>
      <MDBBtn color="primary" @click="updateProduct()">Update Product</MDBBtn>
    </MDBModalFooter>
  </MDBModal>

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
      <p class="my-5">Loading one product...</p>
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
  <Footer />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import axios from "axios";
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
    Navbar,
    Footer,
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

  methods: {
    updateProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://e-commerce-store-finalproject.herokuapp.com/products/" + this.id, {
        method: "PUT",
        body: JSON.stringify({
          title: this.title,
          description: this.description,
          category: this.category,
          price: this.price,
          img_front: this.img_front,
          img_back: this.img_back,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.product = json;
          alert("Product Updated");
          location.reload();
        })
        .catch((err) => {
          alert(err);
        });
    },

    deleteProduct(id) {
      const config = {
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      };
      let apiURL = `https://e-commerce-store-finalproject.herokuapp.com/products//${id}`;

      if (window.confirm("Do you really want to delete?")) {
        axios
          .delete(apiURL, config)
          .then(() => {
            alert("Product Deleted");
            location.reload();
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
};
</script>

<style scoped>
.card .img-top {
  display: none;
  position: absolute;
  top: 18px;
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
</style>
