<template>
  <button @click="click" class="IconButton">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "IconButton",
  props: ["click"]
}
</script>