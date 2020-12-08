<template>
  <v-app>
    <v-main>
      <v-banner elevation="12"
        ><v-toolbar-title>Posts</v-toolbar-title></v-banner
      >
      <v-container class="grey lighten-5">
        <v-row>
          <v-col cols="4" v-for="post in posts" :key="post.id">
            <v-card elevation="2" outlined class="ma-4">
              <v-card-title>{{ post.title }}</v-card-title>
              <v-card-text>{{ post.body }}</v-card-text>
              <v-card-actions>{{ post.userId }}</v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      posts: [],
    };
  },
  async created() {
    try {
      const responsePost = await axios.get(
        `http://jsonplaceholder.typicode.com/posts`
      );

      this.posts = responsePost.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>
