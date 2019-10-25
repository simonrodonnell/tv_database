<template>
  <div id="app">
    <div class="tv-database-header">
      <h1>TV DATABASE</h1>
    </div>
    <div class="components-wrapper">
      <tv-list :shows="shows"></tv-list>
      <tv-item-detail :show="selectedShow"></tv-item-detail>
    </div>
  </div>
</template>

<script>
import TvList from "./components/TvList.vue";
import TvItemDetail from "./components/TvItemDetail.vue";
import { eventBus } from "./main.js";

export default {
  name: 'app',
  data() {
    return {
      shows: [],
      selectedShow: ""
    }
  },
  components: {
    "tv-list": TvList,
    "tv-item-detail": TvItemDetail
  },
  mounted() {
    fetch('https://api.tvmaze.com/shows')
    .then(response => response.json())
    .then(result => this.shows = result);

    eventBus.$on("selected-show", (show) => {
      this.selectedShow = show;
    });
  }
}
</script>

<style>
body {
    background-color: ghostwhite;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.tv-database-wrapper {
  position: fixed;
}

.components-wrapper {
  display: flex;
  /* justify-content: space-evenly; */
}
</style>
