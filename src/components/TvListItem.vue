<template lang="html">
  <div>
    <div id="tv-list-item-wrapper" @click="handleClick">
      <div id="tv-list-item-text">
        <h3>{{show.name}}</h3>
        <h5>Genre: {{show.genres.toString().replace(/,/g, ", ")}}</h5>
        <h5>Rating: {{show.rating.average}}</h5>
      </div>
    </div>
  </div>
</template>


<script>
import { eventBus } from "../main.js";

export default {
  name: "tv-list-item",
  props: ["show"],
  methods: {
    handleClick: function(){
      eventBus.$emit("selected-show", this.show);
    }
  }
}
</script>


<style lang="css" scoped>
h3 {
  margin-top: 6px;
  margin-bottom: 1px;
}

h5 {
  margin: 1px 0;
}

#tv-list-item-wrapper {
  display: flex;
  text-align: center;
  font-size: 14px;
  margin: 10px 10px;
  min-height: 70px;
  border: 2px ridge grey;
  border-radius: 10px;
  background-color: lightgrey;
}

#tv-list-item-text {
  margin: 0 15px;
  text-align: justify;
}

</style>
