<template lang="pug">
  img.button(src="@/assets/button.svg")
</template>

<style lang="stylus" scoped>
.button
  cursor pointer
  transition filter .3s
  &:hover
    filter brightness(92%)
</style>

<script lang="ts">
import 'reflect-metadata';
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Button extends Vue {}
</script>
