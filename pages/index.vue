<template>
  <div class="product">
    <div class="product-image">
      <img v-bind:src="image" v-bind:alt="altText" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock by data</p>
      <p v-else>Out of Stock</p>

      <!-- <span v-if="onSale">On Sale!</span>
      <p v-if="inventory > 10">In Stock by conditional</p>
      <p v-show="inStock">In Stock by v-show</p> -->

      <h3>Details:</h3>
      <ul>
        <li v-for="(detail, index) in details" :key="'datail_'+index">{{ detail }}</li>
      </ul>

      <h3>Sizes:</h3>
      <ul>
        <li v-for="(size, index) in sizes" :key="'size_'+index">{{ size }}</li>
      </ul>

      <h3>Colors:</h3>
      <div v-for="variant in variants" :key="variant.variantId" @mouseover="updateProduct(variant.variantImage)">
        <p>{{ variant.variantColor }}</p>
      </div>

      <button v-on:click="addToCart">Add to cart</button>
      <button @click="removeFromCart">Remove from cart</button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>

    <span>More information: <a href="/pdf/Vue-Essentials-Cheat-Sheet.pdf" target="_blank">Vue-Essentials-Cheat-Sheet</a></span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: 'Socks',
      altText: 'A pair of socks',
      image: '/img/socks-blue.jpg',
      inStock: true,
      onSale: true,
      inventory: 100,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
      variants: [
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: '/img/socks-blue.jpg'
        },
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: '/img/socks-green.jpg'
        }
      ],
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    },
    removeFromCart() {
      this.cart -= this.cart > 0 ?  1 : 0;
    }
  }
};
</script>

<style>
.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}
</style>
