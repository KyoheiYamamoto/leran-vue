<template>
  <v-row>
    <template
      v-if="loading"
    >
        <v-container
          class="px-10 py-10"
          style="text-align:center"
        >
          <v-progress-circular
            size="70"
            color="blue"
            indeterminate
          />
        </v-container>
    </template>
    <template
      v-else
    >
          <v-col
            v-for="item in movieInternalItems"
            :key="item.id"
            cols="12"
            sm="6"
            md="4"
            style="text-align: center"
          >
            <div>
              <iframe :src="item.url" width="290" height="163.25" frameborder="0" />
              <p>{{ item.comment }}</p>
            </div>
          </v-col>
    </template>
  </v-row>
</template>

<script>
export default {
  props: {
    movieItems: {
      type: Array,
      default: null,
    },
    loading: {
      type: Boolean,
      required: true,
      default: true,
    },
  },

  data() {
    return {
      movieInternalItems: [],
    };
  },
  methods: {
    init() {
      this.movieInternalItems = [];
      Object.keys(this.movieItems).forEach((item) => {
        console.log(this.movieItems[item]);
        const newItem = {
          id: this.movieItems[item].id,
          url:"https://www.youtube.com/embed/" +
              this.movieItems[item].url +
              "?controls=1&loop=1&playlist=" +
              this.movieItems[item].url,
          comment: this.movieItems[item].comment,
        };
        this.movieInternalItems.push(newItem);
      });
    },
  },
};
</script>
