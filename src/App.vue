<template>
  <div id="app">
    <div id="col1">
    <h1>Reddit threads?</h1>
      <input id="search" type="text"v-model="search" placeholder="Search Threads">
      <ul v-for="(thread, index) in filteredThreads" :key="index" >
        <reddit-thread :thread="thread"></reddit-thread>

      </ul>
    </div>
  </div>
</template>

<script>

import RedditThread from '@/components/RedditThread';
import {GChart} from 'vue-google-charts';
export default {
  data () {
    return {
      name: 'App',
      redditThreads: [],
      search: ''
    }
  },
  mounted() {
    try {
      let itemHolder = []
      fetch("https://www.reddit.com/r/javascript.json")
          .then(res => res.json())
          .then(response => itemHolder = response.data.children)
          .then(() => itemHolder.forEach(item => this.redditThreads.push(item.data)));
      this.redditFilteredThreads = this.redditThreads;
      console.log('loaded');
    } catch (e) {
      console.log("Failed to load API");
    }
  },
  components: {
    RedditThread
  },
  methods: {
  },
  watch: {
  },
  computed: {
    filteredThreads: function() {
      return this.redditThreads.filter(thread => thread.title.toLowerCase().match(this.search.toLowerCase())) //match means contains
    }
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
}
li {
  list-style-type: none
}
.thread {
  border: 2px solid darkcyan;
  border-left: 2px solid cornflowerblue;
  background-color: antiquewhite;
  opacity: 80%;
}
.thread:hover {
  border: 2px solid cornflowerblue;
  opacity: 100%;
}
#col1 {
  max-width: 45%;
}
#col1 {
  max-width: border-box;
}
h1 {
  padding-left: 60px;
}
#search {
  margin-left: 60px;
}
button > span {
}
</style>

