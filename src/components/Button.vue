<template lang="pug">
img.button(src="@/assets/button.svg" @click="$emit('click')")
</template>

<style lang="stylus" scoped>
.button
  cursor pointer
  transition filter .3s
  &:hover
    filter brightness(92%)
</style>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Button',
  emits: ['click'],
});
</script>
