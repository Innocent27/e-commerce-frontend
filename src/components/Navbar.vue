<template>
  <MDBNavbar id="nav" expand="lg" dark bg="dark" position="top" container-fluid>
    <MDBNavbarToggler
      @click="collapse1 = !collapse1"
      target="#navbarSupportedContent"
    ></MDBNavbarToggler>
    <MDBCollapse v-model="collapse1" id="navbarSupportedContent">
      <ul class="navbar-nav ms-auto d-flex flex-row mt-3 mt-lg-0">
        <li class="nav-item text-center mx-3 mx-lg-1">
          <MDBNavbarNav class="navbar-nav ms-auto d-flex flex-row mt-3 mt-lg-0">
            <MDBNavbarItem>
              <router-link
                class="nav-link"
                href="#!"
                :to="{ name: 'Products' }"
              >
                <div>
                  <i class="fas fa-laptop"></i>
                </div>
                Products
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link
                class="nav-link"
                href="#!"
                :to="{ name: 'Dashboard' }"
              >
                <div>
                  <i class="fas fa-laptop"></i>
                </div>
                Dashboard
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link class="nav-link" href="#!" :to="{ name: 'LoginU' }">
                <div>
                  <i class="fas fa-laptop"></i>
                </div>
                Login
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link
                @click="logout()"
                class="nav-link"
                href="#!"
                :to="{ name: 'LoginU' }"
              >
                <div>
                  <i class="fas fa-laptop"></i>
                </div>
                Logout
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link
                class="nav-link"
                href="#!"
                :to="{ name: 'RegisterU' }"
              >
                <div>
                  <i class="fas fa-laptop"></i>
                </div>
                Register
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link class="nav-link" href="#!" :to="{ name: 'Contact' }">
                <div>
                  <i class="fas fa-phone"></i>
                </div>
                Contact
              </router-link>
            </MDBNavbarItem>

            <MDBNavbarItem>
              <router-link class="nav-link" href="#!" :to="{ name: 'Cart' }">
                <div>
                  <i class="fas fa-shopping-cart"></i>
                </div>
                Cart
              </router-link>
            </MDBNavbarItem>
          </MDBNavbarNav>
        </li>
      </ul>
    </MDBCollapse>
  </MDBNavbar>
</template>
<button class="btn btn-danger" @click="logout()">Logout</button>
<script>
import {
  MDBBtn,
  MDBNavbar,
  MDBNavbarToggler,
  MDBNavbarBrand,
  MDBNavbarNav,
  MDBNavbarItem,
  MDBCollapse,
  MDBDropdown,
  MDBDropdownToggle,
  MDBDropdownMenu,
  MDBDropdownItem,
} from "mdb-vue-ui-kit";
import { ref } from "vue";
export default {
  components: {
    MDBBtn,
    MDBNavbar,
    MDBNavbarToggler,
    MDBNavbarBrand,
    MDBNavbarNav,
    MDBNavbarItem,
    MDBCollapse,
    MDBDropdown,
    MDBDropdownToggle,
    MDBDropdownMenu,
    MDBDropdownItem,
  },
  setup() {
    const collapse1 = ref(false);
    const dropdown1 = ref(false);
    return {
      collapse1,
      dropdown1,
    };
  },
  computed: {
    logout() {
      localStorage.clear();
      alert("User logged out");
    },
  },
};
</script>
<style>
.btn {
  padding: 0.55rem 1.5rem 0.45rem;
}

#nav .a {
  font-weight: bold;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}

#nav .router-link-exact-active {
  color: red;
}

.fas:hover {
  color: rgb(255, 0, 0);
}
</style>
