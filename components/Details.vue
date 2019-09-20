<template>
  <div>
    <h3>{{title}}</h3>
    <ul>
      <li v-for="(detail, index) in details" :key="`${type}_${index}`">{{ detail }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
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
