<template>
  <li class="SlideNavItem">
    <button @click="goTo(index)" :aria-current="isCurrent">
      <span />
    </button>
  </li>
</template>

<script>
export default {
  name: "SlideNavItem",
  props: ["isCurrent", "goTo", "index"]
}
</script>