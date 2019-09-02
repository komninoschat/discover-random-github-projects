<template lang="pug">
  img.spinner(src="@/assets/spinner.png")
</template>

<style lang="stylus" scoped>
.spinner
  animation spin 2s linear infinite

@keyframes spin
  0%
    transform rotate(0deg)
  100%
    transform rotate(360deg)
</style>

<script lang="ts">
import 'reflect-metadata';
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class Spinner extends Vue {}
</script>
