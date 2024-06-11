<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-button @click = "showDialog">Создать пост</my-button>
    <my-dialog v-model:show="dialogVisible"><postForm @create="createPost"/></my-dialog>

    <postList v-if="!isPostsLoading" v-bind:posts="posts" @remove="removePost"/>
    <div v-else>Идёт загрузка...</div>

  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue"
import PostList from "@/components/PostList.vue"
import axios from 'axios';

export default {
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts: [
        // {id: 1, title: 'Javascript', body: 'Описание поста'},
        // {id: 2, title: 'Javascript 2', body: 'Описание поста 2'},
        // {id: 3, title: 'Javascript 3', body: 'Описание поста 3'}
      ],
      dialogVisible: false,
      isPostsLoading: false
    }
  },
  methods: { //функции
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;

          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = response.data;


      } catch (e) {
        alert('Ошибка')
      } finally {
        this.isPostsLoading = false;
      }
    }
  },
  mounted() { //Хук
      this.fetchPosts();
    }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


form {
  display: flex;
  flex-direction: column;
}

.app {
  padding: 20px;
}


</style>
