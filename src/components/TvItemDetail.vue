<template lang="html">
  <div id="tv-item-detail-wrapper">
    <h1>SHOW INFO</h1>
    <div id="tv-item-detail-box">
      <div id="tv-item-detail-text">

        <div id="show-detail-upper">

          <div id="show-info">
            <h1 id="show-name">{{ show.name }}</h1>
            <h3 id="show-genre">Genre: {{show.genres.toString().replace(/,/g, ", ")}}</h3>
            <h3 id="show-country">Country: {{show.network.country.code}}</h3>
            <h3 id="show-network">Network: {{show.network.name}}</h3>
            <h3 id="show-rating">Rating: {{show.rating.average}}</h3>
          </div>

          <div id="show-image-wrapper">
            <img id="show-image" :src="show.image.medium" alt="Show Poster Image">
          </div>

        </div>

        <div id="show-detail-lower">
          <p id="show-summary" v-html="show.summary"></p>
          <button @click="addToWatchlist" id="watchlist-button">ADD TO WATCHLIST</button>
          <a :href="show.officialSite" target="_blank">{{show.officialSite}}</a>
        </div>

      </div>
    </div>
  </div>
</template>


<script>
import { eventBus } from "../main.js";

export default {
  name: "tv-item-detail",
  props: ["show"],
  methods: {
    addToWatchlist: function(){
      eventBus.$emit("watchlist-show", this.show.id);
    }
  }
}
</script>


<style lang="css" scoped>

#tv-item-detail-wrapper {
  text-align: center;
  width: 55%;
  background-color: lightsteelblue;
}

#show-name {
  margin-top: 6px;
  margin-bottom: 1px;
}

h3 {
  margin: 1px 0;
}

#show-detail-upper {
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: space-between;
}

#tv-item-detail-box {
  font-size: 14px;
  border: 2px ridge grey;
  border-radius: 10px;
  background-color: lightgrey;
  margin: 10px;
  padding: 10px;
}

#show-info {
  margin-left: 5px;
  text-align: left;
}

#show-image {
  border-radius: 5px;
  max-height: 140px;
}

#show-detail-lower {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-between;
}

#show-summary {
  height: 80px;
  text-align: justify;
  overflow: auto;
  padding: 0 10px;
  border: 1px solid black;
  border-radius: 5px;
  background-color: darkgrey;
}

#watchlist-button {
  border: 1px solid black;
  border-radius: 5px;
  margin-right: 10px;
}
</style>
