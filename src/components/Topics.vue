<template lang="pug">
  input.topics(placeholder="Add topics (e.g. javascript, go)" :value="value" @input="")
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
import 'reflect-metadata';
import { Component, Vue, Prop, Emit } from 'vue-property-decorator';

@Component
export default class Topics extends Vue {
  @Prop() value!: string;

  @Emit('input')
  emitInput() {
    return this.value;
  }
}
</script>
