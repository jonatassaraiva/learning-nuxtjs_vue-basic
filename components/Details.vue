<template>
  <ul>
    <li v-for="(detail, index) in details" :key="`${type}_${index}`">{{ detail }}</li>
  </ul>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      required: true
    },
    details: {
      type: Array,
      required: true
    }
  }
};
</script>
