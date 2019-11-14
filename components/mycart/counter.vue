<template>
  <span>
    <button @click="increment">-</button>
    {{nums}}
    <button @click="decrement">+</button>
  </span>
</template>

<script>
export default {
  props: {
    nums: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {};
  },
  methods: {
    increment() {
      this.$emit("incre");
    },
    decrement() {
      this.$emit("decre");
    }
  }
};
</script>
