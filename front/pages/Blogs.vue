<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12">
        <v-text-field v-model="blog.title" label="Title"></v-text-field>
        <v-textarea v-model="blog.body" label="Body"></v-textarea>
        <v-btn color="primary" @click="createBlog">Create</v-btn>
      </v-col>
      <v-col cols="12">
        <table>
          <tr>
            <th>Title</th>
            <th>Description</th>
          </tr>
          <tr v-for="blog in blogs" :key="blog.id">
            <td>{{ blog.title }}</td>
            <td>{{ blog.body }}</td>
            <td>show</td>
            <td>Edit</td>
            <td>Destroy</td>
          </tr>
        </table>
      </v-col>
    </v-row>

    <!-- <v-card class="mx-auto" max-width="300" tile>
      <v-list rounded>
        <v-subheader>Blogs</v-subheader>
        <v-list-item-group color="primary">
          <v-list-item v-for="blog in blogs" :key="blogs.id" @click="">
            <v-list-item-content>
              <v-list-item-title v-text="blog.name"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card> -->
  </v-container>
</template>

<script>
import axios from "~/plugins/axios";

export default {
  data() {
    return {
      name: "",
      blog: []
    };
  },
  created() {
    axios.get("/blogs").then(res => {
      if (res.data) {
        this.blogs = res.data;
      }
    });
  },
  methods: {
    createBlog() {
      axios.post("/blogs", { title: this.title, body: this.body }).then(res => {
        if (res.data) {
          this.blogs.push(res.data);
        }
      });
    }
  }
};
</script>
