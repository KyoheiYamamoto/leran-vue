<template>
  <v-container>
    <input-form
      formRounded="xl"
      :formElevation="formElevation"
      @storeMovie="storeMovie"
    />
    <movies
      ref="movies"
      :movie-items="movieItems"
    />
  </v-container>
</template>

<script>
  import InputForm from './InputForm'
  import Movies from './Movies'
  import axios from 'axios'

  export default {
    components: {
      InputForm,
      Movies,
    },

    data () {
      return {
        formElevation: "10",
        movieItems: [{}],
      }
    },

    created() { //pageを実行した瞬間に行われる処理的な・・
       this.getMovies()
    },

    methods: {
      getMovies () {
        axios.get('https://youtube-curation.herokuapp.com/rest/1'
        ).then((response) => {
          this.movieItems = response.data.user.movies
        }).catch((error) => {
          console.log(error)
        }).finally(() => {
          this.$refs.movies.init()
        })
      },
      storeMovie (movieUrl, comment) {
        console.log(movieUrl, comment)
      }
    },
  }
</script>
