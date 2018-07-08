<template>
  <button :disabled="disabled" :class="['btn', `btn-${variation}`]">
    <slot/>
  </button>
</template>

<script>
/**
 */
export default {
  name: "Button",
  status: "prototype",
  release: "1.0.0",
  props: {
    /**
     * Whether the button is disabled or not.
     * `true, false`
     */
    disabled: {
      type: Boolean,
      default: false,
    },
    variation: {
      type: String,
      default: "default",
      validator: value => {
        return value.match(/(default|disabled|primary|warning|)/)
      },
    }
  },
  methods: {
    onInput(value) {
      this.$emit("change", value)
    }
  },
}
</script>

<style lang="scss">
// Design Tokens with local scope
$color-placeholder: tint($color_gray_10, 50%);

.btn {
  border: none;
  border-radius: $border_radius_default;
  color: $color_gray_09;
  font-weight: $font-weight-bold;
  font-family: $font-family-text;
  font-size: $font-size-small;
  line-height: $line-height-heading;
  padding: 0 20px;
  height: 30px;

  &:hover,
  &[hover] {
    box-shadow: none;
    background-color: $color_gray_06;
    cursor: pointer;
  }
  &[disabled] {
    background-color: $color_gray_03;
    color: $color_gray_06;
    cursor: not-allowed;
  }

  &.btn-primary {
    background-color: $color_green_04;
    color: $color_gray_01;
    &:hover {
      background-color: $color_green_05;
    }
    &[disabled] {
      background-color: $color_green_02
    }
  }

}
</style>


<docs>
  ```jsx
  <wrapper>
    <wrapper>
      <heading level="h4">Vue</heading>
      <Button>Default</Button>
      <Button disabled>Disabled</Button>
      <Button variation="primary">Primary</Button>
      <Button variation="primary" disabled>Disabled</Button>
    </wrapper>

    <wrapper>
      <heading level="h4">HTML</heading>
      <button class="btn">Default</button>
      <button class="btn" disabled>Disabled</button>
      <button class="btn btn-primary">Primary</button>
      <button class="btn btn-primary" disabled>Disabled</button>
    </wrapper>
  </wrapper>
  ```
</docs>
