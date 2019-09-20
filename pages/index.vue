<template>
  <div>
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
      <button :class="{ disabledButton: !hasItems }" :disabled="!hasItems" @click="removeFromCart">Remove from cart</button>
    </div>
    <product :premium="premium" @add-to-cart="addToCart" />
  </div>
</template>

<script>
import Product from "@/components/Product";

export default {
  components: {
    Product
  },
  data() {
    return {
      premium: false,
      cart: []
    };
  },
  methods: {
    addToCart(id) {
      this.cart.push(id);
    },
    removeFromCart() {
      this.cart.splice(0, 1);
    }
  },
  computed: {
    hasItems() {
      return this.cart.length > 0;
    }
  }
};
</script>


<style>
.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}
</style>
