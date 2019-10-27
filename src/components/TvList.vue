<template lang="html">
  <div id="tvlist-wrapper">
    <h1 v-if="!selectedGenre">SHOWS</h1>
    <h1 v-else>{{selectedGenre.toUpperCase()}}</h1>
    <select @change="filterTvList" v-model="selectedGenre" >
      <option disabled selected value="">--select genre--</option>
      <option v-for="genre in genres" :value="genre">{{genre}}</option>·
    </select>
    <tv-list-item id="tv-list" v-for="(show, index) in shows" :show="show" :key="index">
    </tv-list-item>
  </div>
</template>


<script>
import TvListItem from "./TvListItem.vue";
import { eventBus } from "../main.js";
export default {
  name: "tv-list",
  data() {
    return {
      selectedGenre: ""
    }
  },
  props: ["shows", "genres"],
  components: {
    "tv-list-item": TvListItem
  },
  methods: {
    filterTvList: function(){
      eventBus.$emit("filter-list", this.selectedGenre);
    }
  }
}
</script>


<style lang="css" scoped>
#tvlist-wrapper {
  background-color: cornflowerblue;
  width: 25%;
}
</style>
