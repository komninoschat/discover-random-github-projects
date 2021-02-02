<template lang="pug">
a(href="https://github.com/komninoschat/discover-github-projects")
  img.github-logo-img(src="@/assets/github.png")
</template>

<style lang="stylus" scoped>
.github-logo-img
    pointer cursor
    border-radius 50%
    border 15px solid rgba(0, 0, 0, 0.2)
    height inherit
    width inherit
</style>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'GithubLogo',
});
</script>
