<template>
  <div class="VueStar">
    <div class="VueStar__ground">
      <div class="VueStar__icon" @click="toggle" :class="AnimateClass" :style='{color:ColorValue}'>
        <slot name="icon"></slot>
      </div>
      <div class="VueStar__decoration" :class="{ 'VueStar__decoration--active':active}"></div>
    </div>
  </div>
</template>

<script>
import { isColors } from '../uitls/colorRE.js'
export default {
  name: 'VueStar',
  props: {
    animate: String,
    color: String,
    active: Boolean,
    unCancel: Boolean,
    index: Number
  },
  methods: {
    toggle () {
      if (this.unCancel) {
        if (!this.active) {
          this.toggleActive = !this.active
          this.toggleAnimate = !this.toggleAnimate
          this.toggleColor = !this.toggleColor
          this.$emit('toggle', this.toggleActive, this.index)
        }
      } else {
        this.toggleActive = !this.active
        this.toggleAnimate = !this.toggleAnimate
        this.toggleColor = !this.toggleColor
        this.$emit('toggle', this.toggleActive, this.index)
      }
    }
  },
  data () {
    return {
      toggleAnimate: false,
      toggleColor: false,
      toggleActive: false
    }
  },
  computed: {
    AnimateClass () {
      return this.active ? this.animate : ''
    },
    ColorValue () {
      return this.active ? this.color : ''
    }
  },
  mounted () {
    if (this.color) {
      if (isColors(this.color)) {
        return
      } else {
        console.error('this color must be hexcolor or rgbcolor  ---VueStar')
      }
    } else {
      return
    }
  }
}
</script>

<style lang="less">
 @import '../style/main.less';
</style>
