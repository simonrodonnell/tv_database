<template lang="html">
  <div>
    <tv-list-item id="tv-list" v-for="(show, index) in shows" :show="show" :key="index">
    </tv-list-item>
  </div>
</template>


<script>
import TvListItem from "./TvListItem.vue";
export default {
  name: "tv-list",
  props: ["shows"],
  components: {
    "tv-list-item": TvListItem
  }
}
</script>


<style lang="css" scoped>
</style>
