<template lang="pug">
input.topics(placeholder="Add topics (e.g. javascript, go)" :value="value" @input="e => this.$emit('input', e.target.value)")
</template>

<style lang="stylus" scoped>
.topics
  width 100%
  font-size 1.3rem
  border-radius 10px
  padding 1.1em 1em
  border 0
  outline 0
  background rgba(0, 0, 0, 0.2)
  color white
  font-weight 500
  &::placeholder
    color rgba(255, 255, 255, 0.65)
</style>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Spinner',
  props: {
    value: {
      type: String,
      default: '',
    },
  },
  emits: ['keyup.enter'],
});
</script>
