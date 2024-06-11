<template>
    <form @submit.prevent>
        <my-input v-model="post.title" type="text" class="input" placeholder="Название"/>
        <my-input v-model="post.body" type="text" class="input" placeholder="Описание"/>
        <my-button @click="createPost">Добавить</my-button>
      </form>
</template>

<script>

export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post) // передача родителю
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}

</script>

<style scoped>



form {
  display: flex;
  flex-direction: column;
}

.app {
  padding: 20px;
}

.btn {
  align-self: flex-end;
  margin-top: 15px;
  /* padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal; */
}
</style>
