<template>
  <product :premium="premium" />
</template>

<script>
import Product from '@/components/Product';

export default {
  components: {
    Product
  },
  data() {
    return {
      premium: false
    }
  }
};
</script>
