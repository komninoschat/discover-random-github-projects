<template lang="pug">
  h1.title
    slot
</template>

<style lang="stylus" scoped>
.title
  text-transform uppercase
  font-size 3.8rem
  color white
  font-weight 500
  text-align center
</style>

<script lang="ts">
import 'reflect-metadata';
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Title extends Vue {}
</script>
