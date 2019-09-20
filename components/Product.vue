<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" :alt="imageAltText" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <p>Shipping: {{ shipping }}</p>

      <Details :title="'Details'" :type="'details'" :details="details" />
      <Details :title="'Sizes'" :type="'size'" :details="sizes" />

      <h3>Colors:</h3>
      <div class="color-box" v-for="(variant, index) in variants"
            :key="variant.variantId"
            :style="{ backgroundColor: variant.variantColor }"
            @mouseover="updateProduct(index)" />

      <button :class="{ disabledButton: !inStock }" :disabled="!inStock" @click="addToCart">Add to cart</button>
    </div>

    <span>More information: <a href="/pdf/Vue-Essentials-Cheat-Sheet.pdf" target="_blank">Vue-Essentials-Cheat-Sheet</a></span>
  </div>
</template>

<script>
import Details from '@/components/Details'

export default {
  components: {
    Details
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      brand: 'Nuxt and Vue',
      product: 'Socks',
      selectedVariant: 0,
      onSale: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
      variants: [
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: '/img/socks-blue.jpg',
          variantImageText: 'Image of blue socks',
          variantQuantity: 10
        },
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: '/img/socks-green.jpg',
          variantImageText: 'Image of green socks',
          variantQuantity: 0
        }
      ]
    };
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
    removeFromCart() {
      this.$emit('remove-from-cart');
    }
  },
  computed: {
    title() {
      return `${this.brand} - ${this.product}`;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    imageAltText() {
      return this.variants[this.selectedVariant].variantImageText;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return "Free"
      }
      return 2.99
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