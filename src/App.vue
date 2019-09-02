<template lang="pug">
  #app
    Overlay(:loading="loading")
    Title.title Discover Random Github Projects
    Topics.topics(v-model="topics" @keyup.native.enter="submit")
    Button.button(@click.native="submit")
    GithubLogo.github-logo
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
  @media (max-width 550px)
    padding 0 15px
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
    max-width 550px
    margin-top 2.5em
    @media (max-width 750px)
      font-size 1rem
  .button
    width 150px
    margin-top 3em
    @media (max-width 600px)
      width 120px
  .github-logo
    position absolute
    right 3.5em
    bottom 2.5em
    height 90px
    @media (max-width 450px)
      position static
      display block
      margin 100px auto 0 auto
</style>

<script lang="ts">
import 'reflect-metadata';
import { Component, Vue } from 'vue-property-decorator';
import Octokit from '@octokit/rest';
import defaultTopics from '@/defaultTopics';
import Button from '@/components/Button.vue';
import GithubLogo from '@/components/GithubLogo.vue';
import Overlay from '@/components/Overlay.vue';
import Spinner from '@/components/Spinner.vue';
import Title from '@/components/Title.vue';
import Topics from '@/components/Topics.vue';

function rng(min: number, max: number) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function rngArray<T>(arr: T[]): T {
  return arr[Math.floor(Math.random() * arr.length)];
}

@Component({
  components: {
    Title,
    Button,
    Topics,
    GithubLogo,
    Overlay,
    Spinner
  }
})
export default class App extends Vue {
  octokit = new Octokit();
  topics: string = '';
  loading: boolean = false;

  async submit() {
    this.loading = true;
    const topics = this.topics.split(',').map(topic => topic.trim());
    const repos = (await this.octokit.search.repos({
      q: (topics.join('+') || rngArray(defaultTopics)) + '&stars:<=400',
      sort: 'updated',
      order: 'desc',
      per_page: 100,
      page: rng(0, 1)
    })).data.items;

    window.open(rngArray(repos.map((repo: any) => repo.html_url)));
    this.loading = false;
  }
}
</script>
