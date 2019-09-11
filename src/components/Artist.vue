<template lang="pug">
 li.artist
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
  name: "Artist",
  props: ["artist"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
li.artist {
  display: block;
  margin: 10px 0;
}
</style>
