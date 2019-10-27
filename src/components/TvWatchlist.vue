<template lang="html">
  <div id="watchlist-wrapper">
    <h1>WATCHLIST</h1>
    <button id="delete-button" @click="clearWatchlist">DELETE ALL</button>
    <tv-list-item id="tv-list" v-for="(show, index) in watchlist" :show="show" :key="index">
    </tv-list-item>
  </div>
</template>

<script>
import TvListItem from "./TvListItem.vue";
import { eventBus } from "../main.js";

export default {
  name: "tv-watchlist",
  props:  ["watchlist"],
  components: {
    "tv-list-item": TvListItem
  },
  methods: {
    clearWatchlist: function(){
      eventBus.$emit("clear-watchlist", this.watchlist);
    }
  }
}
</script>

<style lang="css" scoped>
#watchlist-wrapper {
  width: 25%;
  background-color: cornflowerblue;
}

#delete-button {
  border: 1px solid black;
  border-radius: 5px;
}
</style>
