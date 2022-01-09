<template>
  <div id="app">

    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <a href="#" class="header item">Vuw JS CRUD with Laravel rest api</a>
      </div>
    </div>

    <div class="ui main container">
      <PostCreate :form="form" @onFormSubmit="onFormSubmit" />
      <PostList :posts="posts" @onDelete="onDelete"/>
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import PostCreate from './components/PostCreate.vue';
import PostList from './components/PostList.vue'

export default {
  name: 'App',
  components: {
    PostCreate, PostList
  },
  data(){
    return{
      url: 'http://127.0.0.1:8000/api/posts',
      posts: [],
      form:{title:'', body:'', isEdit:false}
    }
  },
  methods:{
    getPosts(){
      axios.get( this.url).then(data => {
        this.posts = data.data;
      })
    },
    deletePost(id){
      axios.delete(`${this.url}/${id}`).then(() => {
        this.getPosts();
      }).catch(e => {
        alert(e);
      })
    },
    onDelete(id){
      this.deletePost(id);
    },
    createPost(data){
      axios.post(this.url, {
        title:data.title,
        body:data.body
      }).then(()=>{
        this.getPosts();
      }).catch(e=>{
        alert(e);
      })
    },
    onFormSubmit(data){
      // console.log(data);
      if(data.isEdit){
        //Call edit
      }else{
        this.createPost(data);
        this.clearFormData();
      }
    },
    clearFormData(){
      this.form.title = "";
      this.form.body = "";
    }
  },
  created(){
    this.getPosts();
  }
}
</script>

<style>
.vue-color{
  background: #41B883 !important;
}
.main.container{
  margin-top: 60px;
}
.submit-button{
  margin-top: 24px !important;
  float: right;
}
</style>
