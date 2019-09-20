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

    <review @review-submitted="addReview"/>

    <div>
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <ul v-else>
          <li v-for="(review, index) in reviews" :key="index">
            <p>{{ review.name }}</p>
            <p>Rating:{{ review.rating }}</p>
            <p>{{ review.review }}</p>
          </li>
      </ul>
    </div>
    <span>More information: <a href="/pdf/Vue-Essentials-Cheat-Sheet.pdf" target="_blank">Vue-Essentials-Cheat-Sheet</a></span>
  </div>
</template>

<script>
import Details from '@/components/Details'
import Review from '@/components/Review'

export default {
  components: {
    Details,
    Review
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
      ],
      reviews: []
    };
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    },
    addReview(productReview) {
      this.reviews.push(productReview);
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
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}
</style>