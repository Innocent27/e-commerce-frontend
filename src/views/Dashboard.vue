<template>
  <Navbar />
  <!-- Button trigger modal -->
  <MDBModal
    id="exampleModal"
    tabindex="-1"
    labelledby="exampleModalLabel"
    v-model="exampleModal"
  >
    <MDBModalHeader>
      <MDBModalTitle id="exampleModalLabel"> Create Product </MDBModalTitle>
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
          <option value="Samsung">Electronics</option>
          <option value="Huawei">Hardware</option>
          <option value="Apple">Software</option>
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
      <MDBBtn color="secondary" @click="exampleModal = false">Close</MDBBtn>
      <router-link
        :to="{
          name: 'Dashboard',
        }"
        ><MDBBtn color="primary" @click="createProduct()"
          >Create Product</MDBBtn
        ></router-link
      >
    </MDBModalFooter>
  </MDBModal>

  <div class="d-flex justify-content-center mt-4">
    <div class="sortBar mx-1">
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
        <select v-model="selected">
          <option value="">All</option>
          <option value="Electronics">Electronics</option>
          <option value="Huawei">Hardware</option>
          <option value="Apple">Software</option>
        </select>
      </label>
    </div>
    <input type="text" name="all" placeholder="Search" v-model="search" />
  </div>

  <h1 class="fw-bold my-5">Products</h1>
  <MDBBtn
    class="mb-5"
    color="danger"
    aria-controls="exampleModal"
    @click="exampleModal = true"
  >
    Create Product
  </MDBBtn>
  <div class="container border shadow-5-strong py-5">
    <div v-if="products.length" class="row">
      <div
        v-for="product in filterProducts"
        :key="product._id"
        class="product col-xl-4 col-lg-6 col-md-6 col-sm-12 d-flex justify-content-center"
      >
        <router-link
          :to="{
            name: 'OneProduct',
            params: {
              id: product._id,
            },
          }"
        >
          <h2 class="card text-white animate__animated animate__zoomIn">
            <img
              :src="product.img_front"
              class="d-block img-thumbnail"
              alt="..."
            />
            <img
              :src="product.img_back"
              class="img-thumbnail img-top card-img"
              alt="..."
            />
            {{ product.title }}
          </h2>
        </router-link>
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

  <h1 class="fw-bold my-5">Users</h1>
  <input type="text" name="all" placeholder="Search Name" v-model="search1" />
  <div class="container mt-5 border shadow-5-strong py-5">
    <div v-if="users.length" class="row">
      <div
        v-for="user of filterUsers"
        :key="user._id"
        class="product col-xl-4 col-lg-6 col-md-6 col-sm-12 d-flex justify-content-center"
      >
        <router-link
          :to="{
            name: 'UserDetails',
            params: {
              id: user._id,
            },
          }"
        >
          <h2 class="text-white animate__animated animate__zoomIn">
            <img
              src="https://t4.ftcdn.net/jpg/00/64/67/63/360_F_64676383_LdbmhiNM6Ypzb3FM4PPuFP9rHe7ri8Ju.jpg"
              class="d-block img-thumbnail"
              alt="..."
            />
            {{ user.name }}
          </h2>
        </router-link>
      </div>
    </div>
    <div v-else>
      <p class="my-5">Loading users...</p>
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
  MDBModal,
  MDBModalHeader,
  MDBModalTitle,
  MDBModalBody,
  MDBModalFooter,
} from "mdb-vue-ui-kit";
import { ref } from "vue";
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
    MDBModal,
    MDBModalHeader,
    MDBModalTitle,
    MDBModalBody,
    MDBModalFooter,
    Navbar,
    Footer,
  },

  directives: {
    mdbRipple,
  },
  props: ["id"],
  data() {
    return {
      products: [],
      users: [],
      selected: "",
      search: "",
      search1: "",
      title: "",
      category: "",
      description: "",
      img_front: "",
      img_back: "",
      price: "",
      isActive: 0,
    };
  },

  setup() {
    const exampleModal = ref(false);
    return {
      exampleModal,
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
      }),
      fetch("https://e-commerce-store-finalproject.herokuapp.com/users/", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.users = json;
        });
  },

  computed: {
    filterProducts: function () {
      if (this.selected == "") {
        this.products = this.products.filter((product) => {
          return product.category
            .toLowerCase()
            .match(this.selected.toLowerCase());
        });
        if (this.search) {
          this.products = this.products.filter((product) => {
            return product.title.toLowerCase().match(this.search.toLowerCase());
          });
        }
        return this.products;
      }
      if (this.selected) {
        this.products = this.products.filter((product) => {
          return product.category
            .toLowerCase()
            .match(this.selected.toLowerCase());
        });
        if (this.search) {
          this.products = this.products.filter((product) => {
            return product.title.toLowerCase().match(this.search.toLowerCase());
          });
        }
        return this.products;
      }
    },

    // filterUsers: function () {
    //   return this.users.filter((user) => {
    //     return user.name.toLowerCase().match(this.search1.toLowerCase());
    //   });
    // },
  },

  methods: {
    // Create Product
    createProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "LoginU" });
      }
      fetch("https://e-commerce-store-finalproject.herokuapp.com/products/", {
        method: "POST",
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
          location.reload();
          alert("Product Created");
        })
        .catch((err) => {
          alert(err);
        });
    },

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
  },
};
</script>

<style scoped>
@import url(//netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css);

@import url(https://fonts.googleapis.com/css?family=Titillium+Web:300);

.fa-2x {
  font-size: 2em;
}
.fa {
  position: relative;
  display: table-cell;
  width: 60px;
  height: 36px;
  text-align: center;
  vertical-align: middle;
  font-size: 20px;
}

.main-menu:hover,
nav.main-menu.expanded {
  width: 250px;
  overflow: visible;
}

.main-menu {
  background: #212121;
  border-right: 1px solid #e5e5e5;
  position: absolute;
  top: 0;
  bottom: 0;
  height: 100%;
  left: 0;
  width: 60px;
  overflow: hidden;
  -webkit-transition: width 0.05s linear;
  transition: width 0.05s linear;
  transform: translateZ(0) scale(1, 1);
  z-index: 1000;
}

.main-menu > ul {
  margin: 7px 0;
}

.main-menu li {
  position: relative;
  display: block;
  width: 250px;
}

.main-menu li > a {
  position: relative;
  display: table;
  border-collapse: collapse;
  border-spacing: 0;
  color: #999;
  font-family: arial;
  font-size: 14px;
  text-decoration: none;
  transform: translateZ(0) scale(1, 1);
  -webkit-transition: all 0.1s linear;
  transition: all 0.1s linear;
}

.main-menu .nav-icon {
  position: relative;
  display: table-cell;
  width: 60px;
  height: 36px;
  text-align: center;
  vertical-align: middle;
  font-size: 18px;
}

.main-menu .nav-text {
  position: relative;
  display: table-cell;
  vertical-align: middle;
  width: 190px;
  font-family: "Titillium Web", sans-serif;
}

.main-menu > ul.logout {
  position: absolute;
  left: 0;
  bottom: 0;
}

.no-touch .scrollable.hover {
  overflow-y: hidden;
}

.no-touch .scrollable.hover:hover {
  overflow-y: auto;
  overflow: visible;
}

a:hover,
a:focus {
  text-decoration: none;
}

nav {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}

nav ul,
nav li {
  outline: 0;
  margin: 0;
  padding: 0;
}

.main-menu li:hover > a,
nav.main-menu li.active > a,
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus,
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus,
.no-touch .dashboard-page nav.dashboard-menu ul li:hover a,
.dashboard-page nav.dashboard-menu ul li.active a {
  color: #fff;
  background-color: #5fa2db;
}

.area {
  float: left;
  background: #e2e2e2;
  width: auto;
  height: auto;
}

@font-face {
  font-family: "Titillium Web";
  font-style: normal;
  font-weight: 300;
  src: local("Titillium WebLight"), local("TitilliumWeb-Light"),
    url(http://themes.googleusercontent.com/static/fonts/titilliumweb/v2/anMUvcNT0H1YN4FII8wpr24bNCNEoFTpS2BTjF6FB5E.woff)
      format("woff");
}

.product h2 {
  background: #000000;
  padding: 20px;
  border-radius: 10px;
  margin: 10px auto;
  min-width: 350px;
  max-height: 300px;
  cursor: pointer;
  color: #444;
}

.product h2:hover {
  background: rgb(255, 0, 0);
}

.product a {
  text-decoration: none;
}

.card .img-top {
  display: none;
  position: absolute;
  top: 20px;
  left: 75px;
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
</style>
