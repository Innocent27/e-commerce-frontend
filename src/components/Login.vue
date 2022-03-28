<template>
  <div class="container">
    <div class="content">
      <div
        class="login-container animated fadeInDown"
        style="animation-delay: 0.3s"
      >
        <!--   Login   -->
        <div class="login justify-content-center" id="login-form">
          <h1 class="form-title">
            <i class="fas fa-user" style="color: #0000ff"></i> <br />
            LOGIN
            <hr />
          </h1>

          <div
            class="form-container animated fadeIn"
            style="animation-delay: 0.7s"
          >
            <form @submit.prevent="login()">
              <label for=""><i class="fas fa-at"></i> Email </label>
              <input
                type="email"
                name="email"
                v-model="email"
                placeholder="E-mail"
              />

              <label for=""><i class="fab fa-slack-hash"></i> Password </label>
              <input
                type="password"
                name="password"
                v-model="password"
                placeholder="Password"
              />

              <div class="submit-buttons">
                <input type="submit" value="Login" :to="{ name: 'Products' }" />
                <input
                  type="button"
                  value="Sign Up"
                  :to="{ name: 'RegisterU' }"
                  class="btn-register"
                />
              </div>
            </form>
          </div>
        </div>
        <!--   Login   -->
        <div
          class="login animated fadeIn"
          style="animation-delay: 0.7s; animation-duration: 4s"
          id="login-bg"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },

  methods: {
    login() {
      fetch("https://e-commerce-store-finalproject.herokuapp.com/users/", {
        method: "PATCH",
        body: JSON.stringify({
          email: this.email,
          password: this.password,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((res) => res.json())
        .then((json) => {
          // let isAdmin = json.isAdmin;
          // if (isAdmin == true) {
          //   this.$router.push({ name: "Dashboard" });
          // }
          // if (isAdmin == false) {
          //   alert("Not an Admin");
          //   this.$router.push({ name: "ULogin" });
          // }
          localStorage.setItem("jwt", json.jwt);
          alert("User logged in");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert("User does not exsist");
        });
    },
  },
};
</script>
<style scoped>
.content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.login-container {
  background: white;
  position: relative;
  border-radius: 5px;
  display: flex;
  width: 70vw;
  height: 70vh;
  box-shadow: 0 19px 38px rgba(0, 0, 0, 0.07);
  transition: 0.4s;
}

.login {
  transition: 0.4s;
  font-family: Comfortaa;
}

.login#login-form {
  width: 50%;
  display: block;
  padding: 15px;
  align-items: center;
  text-align: center;
  position: relative;
  margin-top: 20px;
}

.login#login-bg {
  width: 50%;
  display: inline-flex;
  /* background: url(https://fscl01.fonpit.de/userfiles/7640001/image/best-high-end-smartphones/AndroidPIT-Best-High-End-Smartphones-Hero-2.jpg); */
  background-size: cover;
  background-position: center center;
  float: right;
  border-radius: 0 5px 5px 0;
}

.form-title {
  position: absolute;
  top: 11%;
  left: 0;
  right: 0;
  text-align: center;
  color: #000000;
  font-size: 2.2em;
  font-family: Spartan;
  line-height: 1.4;
  margin-top: -24px;
}

.form-title hr {
  width: 75%;
  border: 2px solid #dedede1f;
  border-radius: 10px;
  margin-top: 20px;
}

.form-container {
  padding: 25px 10px;
  border-radius: 5px;
  width: 80%;
  text-align: left;
  margin-top: 70px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

label {
  font-size: 0.7em;
  color: #ff0000;
  margin: 0px 0 !important;
  margin-left: 4px !important;
}

input {
  background: #f8fafc;
  border: 0;
  width: 100%;
  display: block;
  padding: 10px 15px;
  border-radius: 5px;
  margin-bottom: 20px !important;
  outline: 0;
  transition: 0.4s;
}

input::placeholder {
  opacity: 0.4;
}

.submit-buttons {
  display: flex;
}

.submit-buttons input {
  width: 50%;
  text-align: center;
  color: rgb(0, 0, 0);
  transition: 0.2s;
}

.submit-buttons input:hover {
  opacity: 0.7;
}

.submit-buttons input:nth-of-type(1) {
  border-radius: 5px 0 0 5px;
  background: #54a0ff;
}

.submit-buttons input:nth-of-type(2) {
  border-radius: 0 5px 5px 0;
  background: #c8d6e5;
}

@media (max-width: 933px) {
  .login#login-bg {
    width: 0;
  }

  .login#login-form,
  .register {
    width: 100%;
  }

  input {
    width: 100%;
  }
}
</style>
