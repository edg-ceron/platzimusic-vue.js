<template>
<li>
  <img :src='artist.image[2]["#text"]' alt="">
  <h2>
    <a :href='artist.url' target='_blank'>{{artist.name}}</a>
  </h2>
</li>
</template>

<script>

export default {
  name: 'artist',
  props: ['artist']
}
</script>

<style scoped>
  li {
    margin: 5px;
    padding: 10px;
    border: 1px solid #2c3e5094;
    border-radius: 5px;
  }
</style>
