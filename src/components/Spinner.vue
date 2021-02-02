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
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Spinner',
});
</script>
