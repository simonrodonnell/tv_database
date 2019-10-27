<template>
  <div id="app">
  <div id="tv-database-header">
    <h1>📺 CODECLAN TV DATABASE 📺</h1>
  </div>
  <div class="components-wrapper">

    <tv-list v-if="filterShows.length > 0" :genres="genres" :shows="filterShows"></tv-list>
    <tv-list v-else :genres="genres" :shows="allShows"></tv-list>

    <tv-item-detail v-if="selectedShow" :show="selectedShow"></tv-item-detail>

    <tv-watchlist  v-if="watchlist.length > 0" :watchlist="watchlist"></tv-watchlist>
  </div>
</div>
</template>

<script>
import TvList from "./components/TvList.vue";
import TvItemDetail from "./components/TvItemDetail.vue";
import TvWatchlist from "./components/TvWatchlist.vue";
import { eventBus } from "./main.js";

export default {
  name: 'app',
  data() {
    return {
      allShows: [],
      filterShows: [],
      watchlist: [],
      selectedShow: ""
    }
  },
  computed: {
    genres: function() {
      const tempArray = this.allShows.map((show) => {
        return show.genres
      });
      const allGenres = tempArray.flat();
      return allGenres.filter((genre, index) => {
        return allGenres.indexOf(genre) === index;
      })
    }
  },
  components: {
    "tv-list": TvList,
    "tv-item-detail": TvItemDetail,
    "tv-watchlist": TvWatchlist
  },
  methods: {
    makeFilterAll: function(){
      this.filterShows = this.allShows;
    }
  },
  mounted() {
    fetch('https://api.tvmaze.com/shows')
    .then(response => response.json())
    .then(result => (this.allShows = result));

    eventBus.$on("selected-show", (show) => {
      this.selectedShow = show;
    });

    eventBus.$on("clear-watchlist", (watchlist) => {
      this.watchlist = [];
    });

    eventBus.$on("filter-list", (genre) => {
      this.filterShows = this.allShows.filter((show) => {
        return show.genres.flat().includes(genre)
      })
    });

    eventBus.$on("watchlist-show", (id) => {
      let newShow = this.allShows.find((show) => {
        return show.id === id;
      });
      if ( !this.watchlist.includes(newShow) ) {
        this.watchlist.push(newShow);
      }
    });
  }
}
</script>

<style>
body {
  background-color: lightgrey;
}

#tv-database-header {
  background-color: lightsteelblue;
  margin: 20px auto;
  padding: 10px;
  width: 50%;
  border: 4px ridge darkgrey;
  border-radius: 5px
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

.components-wrapper {
  display: flex;
  flex-direction: row;
  /* justify-content: space-evenly;  */
}
</style>
