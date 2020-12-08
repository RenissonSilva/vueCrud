<template>
  <v-app>
    <v-main>
      <v-banner elevation="3">
        <v-avatar slot="icon" color="white accent-4" size="40">
          <v-icon icon="mdi-lock" color="blue">
            mdi-twitter
          </v-icon> </v-avatar
        ><v-toolbar-title>Twitter</v-toolbar-title></v-banner
      >
      <v-container>
        <v-row>
          <v-col cols="4" v-for="post in posts" :key="post.id">
            <v-card
              elevation="6"
              outlined
              class="ma-4 white--text"
              color="blue lighten-2"
            >
              <v-card-title class="body-1 font-weight-bold">{{
                post.title
              }}</v-card-title>
              <v-card-text class="body-2 white--text">{{
                post.body
              }}</v-card-text>
              <v-card-actions>
                <v-card-text text="teste">{{ post.userId }} </v-card-text
                ><v-avatar color="white" size="60">
                  <img :src="getPhoto(`${post.userId}`)" /> </v-avatar
              ></v-card-actions>
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
  methods: {
    getPhoto(id) {
      return `https://pokeres.bastionbot.org/images/pokemon/${id}.png`;
    },
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
