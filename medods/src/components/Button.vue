<template>
  <div
    class="button"
    :style="{ background: color, opacity: '0.6' }"
    :class="{ active: press }"
    @click="pressed"
  >
  </div>
</template>

<script>
export default {
  props: ["color"],
  data: () => {
    return {
      press: false,
    };
  },
  methods: {
    pressed() {
      if (this.press) {
        return;
      }
      console.log(this.color);
      this.press = true;
      setTimeout(() => {
        this.press = false;
      }, 1000);
    },
  },
};
</script>

<style>
.button {
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: black;
  cursor: pointer;
}
.active {
  opacity: 1!important;
}
</style>
