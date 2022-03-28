<template>
  <Navbar />
  <div class="container my-5">
    <h1 class="fw-bold mb-5">Products</h1>
    <div class="d-flex justify-content-center">
      <div class="sortBar">
        <label>
          Sort Price:
          <select v-model="price" @change="sortPrice(price)">
            <option value="asc">Ascending</option>
            <option value="desc">Descending</option>
          </select>
        </label>
        <label>
          Sort Name:
          <select v-model="title" @change="sortTitle(title)">
            <option value="asc">Ascending</option>
            <option value="desc">Descending</option>
          </select>
        </label>
        <label>
          Filter Category:
          <select v-model="category" @change="filterCategory(category)">
            <option value="">All</option>
            <option value="Electronics">Electronics</option>
            <option value="Software">Software</option>
            <option value="Hardware">Hardware</option>
          </select>
        </label>
      </div>
      <input
        type="text"
        name="all"
        placeholder="Search Category"
        v-model="search"
      />
    </div>

    <div v-if="products.length" class="row">
      <div
        v-for="product of filterProducts"
        :key="product._id"
        class="col-lg-4 col-md-6 col-sm-12 d-flex justify-content-center"
      >
        <MDBCard text="danger" bg="dark" class="border shadow-5-strong my-5">
          <a class="card" v-mdb-ripple="{ color: 'dark' }">
            <MDBCardImg
              :src="product.img_front"
              class="card-img"
              alt="Card Front"
            />
            <MDBCardImg
              :src="product.img_back"
              class="img-top card-img"
              alt="Card Back"
            />
          </a>
          <MDBCardBody>
            <MDBCardTitle>{{ product.title }}</MDBCardTitle>
            <MDBCardText> {{ product.category }} </MDBCardText>
            <MDBCardText>R{{ product.price }} </MDBCardText>
            <router-link
              :to="{
                name: 'ProductDetails',
                params: {
                  id: product._id,
                },
              }"
              ><MDBBtn tag="a" href="#!" color="info"
                >View Product</MDBBtn
              ></router-link
            >
            <MDBBtn tag="a" href="#!" color="success">Button</MDBBtn>
          </MDBCardBody>
        </MDBCard>
      </div>
    </div>
    <div v-else>
      <p class="my-5">Loading products...</p>
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
import Carousel from "@/components/Carousel.vue";
import {
  MDBCard,
  MDBCardBody,
  MDBCardTitle,
  MDBCardText,
  MDBCardImg,
  MDBBtn,
  mdbRipple,
  MDBCardGroup,
  MDBCardGroupItem,
} from "mdb-vue-ui-kit";

export default {
  components: {
    MDBCard,
    MDBCardBody,
    MDBCardTitle,
    MDBCardText,
    MDBCardImg,
    MDBBtn,
    MDBCardGroup,
    MDBCardGroupItem,
    Carousel,
    Navbar,
    Footer,
  },

  directives: {
    mdbRipple,
  },
  data() {
    return {
      products: [],
      search: "",
      category: "",
      price: "",
      title: "",
    };
  },
  mounted() {
    fetch("https://e-commerce-store-finalproject.herokuapp.com/products/", {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
      },
    })
      .then((response) => response.json())
      .then((json) => {
        this.products = json;
      });
  },

  // computed: {
  //   filterProducts: function () {
  //     return this.products.filter((product) => {
  //       return product.title.toLowerCase().match(this.search.toLowerCase());
  //     });
  //   },
  // },

  computed: {
    filterProducts: function () {
      return this.products.filter((product) => {
        return product.category.toLowerCase().match(this.search.toLowerCase());
      });
    },
  },

  methods: {
    sortPrice(price) {
      this.filterProducts = this.filterProducts.sort(
        (a, b) => a.price - b.price
      );
      if (price == "desc") this.filterProducts.reverse();
    },

    sortTitle(title) {
      this.filterProducts = this.filterProducts.sort((a, b) => {
        if (a.title.toLowerCase() < b.title.toLowerCase()) {
          return -1;
        }
        if (a.title.toLowerCase() > b.title.toLowerCase()) {
          return 1;
        }
        return 0;
      });
      if (title == "desc") this.filterProducts.reverse();
    },

    filterCategory(category) {
      if (category) {
        this.filterProducts = this.products.filter(
          (product) => product.category == category
        );
      } else {
        this.filterProducts = this.products;
      }
    },
  },
};
</script>

<style>
.products {
  min-height: 50vh;
}
</style>
