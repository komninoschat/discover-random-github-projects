<template lang="pug">
.overlay(:style="{opacity: loading ? '1' : '0', pointerEvents: loading ? 'all' : 'none'}")
  Spinner.spinner
</template>

<style lang="stylus" scoped>
.overlay
  z-index 100
  position absolute
  top 0
  right 0
  bottom 0
  left 0
  background rgba(0, 0, 0, .6)
  display flex
  align-items center
  justify-content center
  transition opacity .3s
  .spinner
    height 120px
    @media (max-width 500px)
      height 100px
</style>

<script lang="ts">
import { defineComponent } from 'vue';

import Spinner from '@/components/Spinner.vue';

export default defineComponent({
  name: 'Overlay',
  components: {
    Spinner,
  },
  props: {
    loading: {
      type: Boolean,
      default: false,
    },
  },
});
</script>
