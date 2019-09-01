<template lang="pug">
  #app
    h1.title Discover Random Github Projects
    input.topics(placeholder="Add topics (e.g. javascript, go)" v-model="topics")
    img.button(src="@/assets/button.svg" @click="submit")
</template>

<style lang="stylus">

* {
  box-sizing border-box
}

#app
  font-family 'Oswald', sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  min-height 100vh
  background #DB24A5
  display flex
  flex-direction column
  align-items center
  .title
    text-transform uppercase
    font-size 3.8rem
    color white
    margin-top 2em
    font-weight 500
    text-align center
    @media (max-width 900px)
      font-size 3em
  .topics
    width 100%
    max-width 550px
    margin-top 2.5em
    margin-left 1em
    margin-right 1em
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
    @media (max-width 750px)
      font-size 1rem
  .button
    cursor pointer
    width 150px
    margin-top 3em
    transition filter .3s
    &:hover
      filter brightness(92%)
    @media (max-width 600px)
      width 120px
</style>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class App extends Vue {
  topics: string = "";

  submit() {
    const topics = this.topics.split(",").map(topic => topic.trim());
  }
}
</script>
