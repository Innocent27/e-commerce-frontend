<template>
  <MDBCarousel
    v-model="carousel6"
    :items="items6"
    :indicators="false"
    fade
    dark
    class="carousel"
  />
</template>

<script>
import { ref } from "vue";
import { MDBCarousel } from "mdb-vue-ui-kit";
export default {
  components: {
    MDBCarousel,
  },
  setup() {
    const items6 = [
      {
        // src: "https://www.smartphonevalley.com.bd/images/products/Untitled-11644742870.jpg",
        // alt: "Samsung",
        // label: "Samsung Galaxy S22+",
        // caption: "Samsung's Flagship Range Smartphone",
      },
      {
        // src: "https://media.takealot.com/covers_images/eb76e342e72145d19abf645b0003ef11/s-pdpxl.file",
        // alt: "Huawei",
        // label: "Huawei P40",
        // caption: "Huawei's Flagship Range Smartphone",
      },
      {
        // src: "https://www.everyshop.co.za/media/catalog/product/cache/ea1c1d49663f18175f3f3520f39859aa/i/p/iphone_13_pro_max_sierra_blue_pure_back_iphone__512gb_a566.jpg",
        // alt: "iPhone",
        // label: "Apple iPhone 13 Pro Max",
        // caption: "Apple's Flagship Range Smartphone",
      },
    ];
    const carousel6 = ref(0);
    return {
      items6,
      carousel6,
    };
  },
};
</script>

<style>
.carousel {
  max-height: 300px;
  max-width: 300px;
  display: inline-block;
}

/* .products {
  display: inline-block;
  justify-content: center;
} */
</style>
