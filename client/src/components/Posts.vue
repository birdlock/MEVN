<template>
<b-container class="bv-example-row">
  <b-row>
    <b-col></b-col>
    <b-col>
         <h1>Posts</h1>
    <div v-if="posts.length > 0" class="table-wrap">
      <div>
        <router-link  v-bind:to="{ name: 'NewPost' }" class="add_post_link">Add Post</router-link>
      </div>
      <br>

      <table width="100%">
        <tr>
          <td align="center">Title</td>
          <td  align="center">Description</td>
          <td  align="center">Action</td>
        </tr>
        <tr v-for="post in posts" :key="post.id">
          <td>{{ post.title }}</td>
          <td>{{ post.description }}</td>
          <td align="center">
            <router-link v-bind:to="{ name: 'EditPost', params: { id: post._id } }">Edit</router-link> |
            <a href="#" @click="deletePost(post._id)">Delete</a>
          </td>
        </tr>
      </table>

    </div>
    <div v-else>
      There are no posts.. Lets add one now <br /><br />
      <router-link v-bind:to="{ name: 'NewPost' }" class="add_post_link">Add Post</router-link>
    </div>
    </b-col>
    <b-col></b-col>
  </b-row>
</b-container>
</template>

<script>
import PostsService from '@/services/Postservice'
export default {
  name: 'posts',
  data () {
    return {
      posts: []
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    async getPosts () {
      const response = await PostsService.fetchPosts()
      this.posts = response.data.posts
    },
    async deletePost (id) {
      await PostsService.deletePost(id)
      this.$router.push({ name: 'Posts' })
      this.getPosts()
    }
  }
}
</script>
<style type="text/css">
.table-wrap {
  width: 100%;
  margin: 0 auto;
  text-align: center;
}
table th, table tr {
  text-align: left;
}
table thead {
  background: #f2f2f2;
}
table tr td {
  padding: 10px;
}
table tr:nth-child(odd) {
  background: #f2f2f2;
}
table tr:nth-child(1) {
  background: #4d7ef7;
  color: #fff;
}
a {
  color: #4d7ef7;
  text-decoration: none;
}
a.add_post_link {
  background: #4d7ef7;
  color: #fff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
}
.app_post_btn {
  background: #4d7ef7;
  color: #fff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
  width: 520px;
  border: none;
  cursor: pointer;
}
</style>
