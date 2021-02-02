<template lang="pug">
#app
  Overlay(:loading="loading")
  Title.title Discover Random Github Projects
  Topics.topics(v-model="topics" @keyup.enter="submit")
  Button.button(@click="submit")
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
    @media (max-width 550px)
      font-size 2.5em
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
</style>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';

import { Octokit } from '@octokit/rest';
import { isMobile } from 'mobile-device-detect';

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

export default defineComponent({
  name: 'App',
  components: {
    Title,
    Button,
    Topics,
    GithubLogo,
    Overlay,
    Spinner,
  },
  setup() {
    const topics = ref('');
    const loading = ref(false);
    const octokit = ref(new Octokit());

    const loadLocalStorageTopics = onMounted(function() {
      if (localStorage.topics) {
        topics.value = localStorage.topics;
      }
    });

    async function submit() {
      loading.value = true;
      localStorage.topics = topics;
      const topicsArray = topics.value
        .split(',')
        .map(topic => topic.trim())
        .map(topic => {
          if (topic === 'c++') return 'cpp';
          else if (topic === 'c#') return 'csharp';
          else return topic;
        });
      const repos = await octokit.value.search
        .repos({
          q: (topicsArray.join('+') || rngArray(defaultTopics)) + ' stars:>=20',
          sort: 'updated',
          order: 'desc',
          // eslint-disable-next-line
        per_page: 100,
          page: rng(0, 1),
        })
        .then((res: any) => res.data.items);

      const url = rngArray<string>(repos.map((repo: any) => repo.html_url));
      if (isMobile) {
        window.location.href = url;
      } else {
        window.open(url);
      }
      loading.value = false;
    }

    return {
      loadLocalStorageTopics,
      submit,
      topics,
      loading,
      octokit,
    };
  },
});
</script>
