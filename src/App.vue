<template>
  <v-app>
    <!-- ヘッダーの部分 -->
    <v-toolbar
      dark
      src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
      max-height="60"
    >
      <v-toolbar-title>YouTube Curation</v-toolbar-title>
    </v-toolbar>
    
    <!-- topコンポーネント -->
    <top />

    <!-- フッター -->
    <v-toolbar dark src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg">
      <v-spacer />
      <p>@QuestAcademia</p>
    </v-toolbar>
  </v-app>
</template>

<script>
import Top from "./components/Top.vue";

export default {
  name: "App",
  components: {
    Top,
  },
};
</script>

<style></style>
