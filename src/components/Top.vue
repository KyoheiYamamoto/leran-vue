<template>
  <v-container>
    <input-form
      formRounded="xl"
      :formElevation="formElevation"
      @storeMovie="storeMovie"
    />
    <v-messages
      :value="responseError"
      color="red"
      class="response-error my-5 text-center"

    />
    <movies
      ref="movies"
      :movie-items="movieItems"
      :loading="loading"
    />
    <!-- loadingはpropsで渡している -->
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
        responseError: [],
        loading:true,
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
          this.responseError = ['動画の取得に失敗しました']
          console.log(error)
        }).finally(() => {
          setTimeout(() => {
            this.loading = false
          }, 1000);
          this.$refs.movies.init()
        })
      },
      storeMovie (movieUrl, comment) {
        console.log(movieUrl, comment)
      }
    },
  }
</script>

<style>
  .response-error .v-messages__message {
    font-size: 18px
  }
</style>
