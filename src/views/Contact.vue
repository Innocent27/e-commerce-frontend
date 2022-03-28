<template>
  <Navbar />
  <div class="container">
    <div class="content">
      <div
        class="login-container animated fadeInDown"
        style="animation-delay: 0.3s"
      >
        <!--   Login   -->
        <div class="contact justify-content-center" id="contact-form">
          <h1 class="form-title">
            <i class="fas fa-user" style="color: #0000ff"></i> <br />
            CONTACT
            <hr />
          </h1>

          <div
            class="form-container animated fadeIn"
            style="animation-delay: 0.7s"
          >
            <form @submit.prevent="handleSubmit()">
              <label for="name"><i class="fas fa-at"></i> Name </label>
              <input
                type="text"
                name="name"
                v-model="name"
                placeholder="Name"
              />

              <label for="email"><i class="fas fa-at"></i> Email </label>
              <input
                type="email"
                name="email"
                v-model="email"
                placeholder="Email"
              />

              <label for="message"><i class="fas fa-at"></i> Message</label>
              <input
                class="textarea"
                type="textarea"
                name="message"
                v-model="textarea"
                placeholder="Message"
              />

              <div class="submit-buttons">
                <input type="submit" value="Send" />
                <input type="reset" value="Reset" class="btn-contact" />
              </div>
            </form>
          </div>
        </div>
        <!--   Login   -->
        <div
          class="contact animated fadeIn"
          style="animation-delay: 0.7s; animation-duration: 4s"
          id="contact-bg"
        ></div>
      </div>
    </div>
  </div>
  <Footer />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
export default {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      name: "",
      email: "",
      textarea: "",
    };
  },

  methods: {
    handleSubmit() {
      fetch("https://e-commerce-store-finalproject.herokuapp.com/contact", {
        method: "POST",
        body: JSON.stringify({
          name: this.name,
          email: this.email,
          textarea: this.textarea,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((res) => res.json())
        .then((data) => (this.contact = data));
      alert("Message Sent!").catch((err) => console.log(err.message));
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

.contact#contact-form {
  width: 50%;
  display: block;
  padding: 15px;
  align-items: center;
  text-align: center;
  position: relative;
  margin-top: 20px;
}

.contact#contact-bg {
  width: 50%;
  display: inline-flex;
  /* background: url(https://sm.mashable.com/t/mashable_sea/image/t/the-best-c/the-best-cyber-monday-smartphone-deals-are-right-here_ejs9.1248.jpg); */
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
  color: rgb(0, 0, 0);
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
  color: red;
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

  .textarea {
    width: 100%;
    height: 150px;
    padding: 12px 20px;
    box-sizing: border-box;
    border-radius: 4px;
    background-color: #f8f8f8;
    font-size: 16px;
    resize: none;
  }
}
</style>
