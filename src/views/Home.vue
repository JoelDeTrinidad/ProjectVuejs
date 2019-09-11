<template lang="pug">
.home
 img(alt='Vue logo', src='../assets/logo.png')
 h1 All  the  artists  of country 
 Spinner(v-show="loading")
 select(v-model="selectCountry")
  option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
 Artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
// @ is an alias to /src
import Artist from "@/components/Artist.vue";
import Spinner from "@/components/Spinner.vue";
import getArtists from "../api";
export default {
  name: "home",
  components: {
    Artist,
    Spinner
  },
  data() {
    return {
      artists: [],
      countries: [
        { name: "Nicaragua", value: "nicaragua" },
        { name: "Argentina", value: "argentina" },
        { name: "España", value: "spain" }
      ],
      selectCountry: "nicaragua",
      loading: false
    };
  },
  methods: {
    refreshArthis() {
      this.loading = true;
      this.artists = [];
      const self = this;
      getArtists(this.selectCountry).then(function(artists) {
        self.artists = artists;
        self.loading = false;
      });
    }
  },
  mounted() {
    this.refreshArthis();
  },
  watch: {
    selectCountry() {
      this.refreshArthis();
    }
  }
};
</script>
<style scoped lang="stylus">
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
