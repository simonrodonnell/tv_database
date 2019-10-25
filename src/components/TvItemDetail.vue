<template lang="html">
  <div>
    <div id="tv-item-detail-wrapper">
      <div id="tv-item-detail-text">
        <h1 id="show-name">{{ show.name }}</h1>
        <div id="show-info">
          <h3>Genre: {{show.genres.toString().replace(/,/g, ", ")}}</h3>
          <h3>Country: {{show.network.country.code}}</h3>
          <h3>Network: {{show.network.name}}</h3>
          <h3>Rating: {{show.rating.average}}</h3>
          <p id="show-summary" v-html="show.summary"></p>
        </div>
        <a :href="show.officialSite" target="_blank">{{show.officialSite}}</a>
      </div>
      <div id="show-image-wrapper">
        <img id="show-image" :src="show.image.medium" alt="">
        <!-- <button>❤️</button> -->
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "tv-item-detail",
  props: ["show"]
}
</script>


<style lang="css" scoped>
h1 {
  margin-top: 6px;
  margin-bottom: 1px;
}

h3 {
  margin: 1px 0;
}

#tv-item-detail-wrapper {
  display: flex;
  text-align: center;
  font-size: 14px;
  margin: 10px 20px;
  height: 320px;
  border: 2px ridge grey;
  border-radius: 10px;
  background-color: lightgrey;
  position: fixed;
}

#tv-item-detail-text {
  margin: 10px;
  padding: 10px;
  text-align: justify;
}

#show-summary {
  height: 80px;
  max-width: 500px;
  overflow: auto;
  padding: 10px;
  border: 2px ridge grey;
  border-radius: 5px;
  background-color: darkgrey;
}

#show-image-wrapper {
  display: flex;
  align-items: center;
}

#show-image {
  margin: 10px;
  border-radius: 5px;
  max-height: 280px;
}
</style>
