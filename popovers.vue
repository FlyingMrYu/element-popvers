<template>
  <transition :name="transition">
    <div
      v-show="visible"
      :class="className"
      :style="style"
      :data-popover="this.name"
      @click.stop
      ref="dropdown"
    >
      <slot></slot>
    </div>
  </transition>
</template>
<script>
export default {
  name: "Popover",
  props: {
    transition: {
      type: String,
      default: "fade-in-linear"
    },
    width: {
      type: Number,
      default: 200
    },
    top: {
      required: true
    },
    left: {
      required: true
    },
    visible: {
      type: Boolean,
      required: true,
      default: false
    },
    cassName:{
      default: 'dropdown-position-bottom'
    },
  },
  data() {
    return {
      zIndex: 99,
    };
  },
  computed: {
    className() {
      // return ["vue-popover", "dropdown-position-bottom"];
      return ["vue-popover", this.cassName];
    },
    style() {
      const { width, zIndex, top, left } = this;
      const styles = {
        position: "absolute",
        width: `${width}px`,
        top: `${top * 1 + 30}px`,
        left: `${left * 1 - 120}px`,
        zIndex
      };
      return styles;
    }
  },
  methods: {
  }
};
</script>
<style scoped lang="scss">
$pointer-size: 6px;

.vue-popover {
  display: block;
  position: absolute;
  background: #fff;
  padding: 10px 20px;
  box-shadow: 0px 4px 20px 0px rgba(52, 73, 94, 0.2);
  border-radius: 5px;
  z-index: 99;
  &:before {
    display: block;
    position: absolute;
    width: 0;
    height: 0;
    content: "";
  }
  &.dropdown-position-bottom:before {
    border-left: $pointer-size solid transparent;
    border-right: $pointer-size solid transparent;
    border-bottom: $pointer-size solid #fff;
    top: -$pointer-size;
    left: calc(50% - #{$pointer-size});
    filter: drop-shadow(0px -2px 2px rgba(52, 73, 94, 0.1));
  }
  &.dropdown-position-top:before {
    border-left: $pointer-size solid transparent;
    border-right: $pointer-size solid transparent;
    border-top: $pointer-size solid #fff;
    bottom: -$pointer-size;
    left: calc(50% - #{$pointer-size});
    filter: drop-shadow(0px 2px 2px rgba(52, 73, 94, 0.1));
  }
  &.dropdown-position-left:before {
    border-top: $pointer-size solid transparent;
    border-bottom: $pointer-size solid transparent;
    border-left: $pointer-size solid #fff;
    right: -$pointer-size;
    top: calc(50% - #{$pointer-size});
    filter: drop-shadow(2px 0px 2px rgba(52, 73, 94, 0.1));
  }
  &.dropdown-position-right:before {
    border-top: $pointer-size solid transparent;
    border-bottom: $pointer-size solid transparent;
    border-right: $pointer-size solid #fff;
    left: -$pointer-size;
    top: calc(50% - #{$pointer-size});
    filter: drop-shadow(-2px 0px 2px rgba(52, 73, 94, 0.1));
  }
 
}
</style>
