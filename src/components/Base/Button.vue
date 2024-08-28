<template>
  <button class="btn" :class="{disabled}" @click.prevent="click">
    {{ title }}
  </button>
</template>

<script>
export default {
    name: "Button",
    props: ["title", "click", "disabled"]
}
</script>