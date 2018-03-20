<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Platimusic</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" v-bind:value="country.value">{{country.name}}</option>
    </select>
    <Spinner v-show='loading'/>
    <ul>
      <Artist v-for='artist in artists' v-bind:artist="artist" v-bind:key='artist.mbid'></Artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/artist'
import getArtists from './api/index'
import Spinner from './components/spinner'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Mexico', value:'mexico' },
        {name: 'colombia', value:'colombia' },
        {name: 'España', value:'spain' },
        {name: 'Alemania', value:'germany' },
        {name: 'Andorra', value:'andorra' },
      ],
      selectedCountry: 'mexico',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtist () {
      const _this = this
      this.loading = true
      this.artists = []
    getArtists(this.selectedCountry)
      .then(function (artists) {
        _this.loading = false
        _this.artists = artists
      })
    }
  },
  mounted: function () {
      this.refreshArtist()
  },
  watch: {
    selectedCountry: function () {
      this.refreshArtist()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  padding: 5%;
  background: #8080801a;
}

li {
  display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 0 1 calc(18% - 1em);
}

a {
  color: #42b983;
}
</style>
