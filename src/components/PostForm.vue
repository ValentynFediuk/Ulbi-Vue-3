<template>
  <form @submit.prevent>
    <h4>Post creation</h4>
    <my-input
        v-model="post.title"
        type="text"
        placeholder="Name"
    />
    <my-input
        v-model="post.body"
        type="text"
        placeholder="Description"
    />
    <my-button
        @click="createPost"
        style="align-self: flex-end; margin-top: 15px"
    >
      Create post
    </my-button>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
import MyInput from "@/components/UI/MyInput";
export default {
  components: {MyInput, MyButton},
  data() {
    return {
      post: {
        title: '',
        body: '',
        selectedFile: null,
      }
    }
  },
  methods: {
    createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post, 'second param', 'third param');
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
</style>