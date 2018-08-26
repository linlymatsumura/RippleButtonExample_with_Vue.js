<template>
  <button
    type="button"
    class="myButton"
    @click="onClick"
    :disabled="ripple"
  >
    <transition
      name="ripple"
      @enter="rippleEnter"
      @after-enter="afterRippleEnter"
    >
      <span
        v-if="ripple"
        ref="ripple"
        class="ripple"
      />
    </transition>
    <span class="label">
      <slot>BUTTON LABEL</slot>
    </span>
  </button>
</template>

<script>
export default {
  data() {
    return {
      ripple: false,
      x: 0,
      y: 0
    };
  },
  methods: {
    onClick(e) {
      this.x = e.layerX;
      this.y = e.layerY;
      this.ripple = !this.ripple;
      this.$emit("click");
    },
    rippleEnter() {
      this.$refs.ripple.style.top = `${this.y}px`;
      this.$refs.ripple.style.left = `${this.x}px`;
    },
    afterRippleEnter() {
      this.ripple = false;
    }
  }
};
</script>

<style lang="scss" scoped>
$button-color: skyblue;

.myButton {
  border: none;
  position: relative;
  font-size: 16px;
  padding: 10px 30px;
  border-radius: 4px;
  overflow: hidden;
  background-color: $button-color;
  cursor: pointer;
  transition: background-color 0.2s;
  &:hover {
    background-color: darken($button-color, 10%);
    .label {
      transform: translateY(1px);
    }
  }
  &:focus {
    outline: none;
  }
  &:disabled {
    background-color: darken($button-color, 10%);
    .label {
      opacity: 0.5;
      transform: translateY(1px);
    }
  }
}
.label {
  display: block;
  pointer-events: none;
  color: white;
  transform: translateY(0);
  transition: transform 0.2s;
}
.ripple {
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 10px;
  position: absolute;
  top: 0;
  left: 0;
  pointer-events: none;
  background-color: rgba(lighten($button-color, 20%), 0.8);
  opacity: 0;
  transform: translate(-50%, -50%) scale(10);
  transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
  &-enter {
    opacity: 1;
    transform: translate(-50%, -50%) scale(0);
  }
}
</style>
