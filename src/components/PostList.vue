<template>
  <div class="post-list">
      <div class="data">
          <table class="ui celled table">
              <thead>
                  <tr>
                      <th>#</th>
                      <th>Title</th>
                      <th>Body</th>
                      <th>Actions</th>
                  </tr>
              </thead>
              <tbody>
                  <Post v-for="post in posts" :key="post.id" :post="(post)" @onDelete="onDelete"/>
              </tbody>
          </table>
      </div>
  </div>
</template>

<script>
import Post from './Post';
export default {
    name: "PostList",
    components:{
        Post
    },
    props:{
        posts:{
            type: Array
        }
    },
    methods:{
        onDelete(id){
            this.$emit('onDelete', id);
        }
    }
}
</script>

<style>

</style>