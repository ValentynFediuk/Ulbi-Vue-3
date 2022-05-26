<template>
  <div v-show="posts.length > 0">
    <h3 class="title">Post list</h3>
    <post-item
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
    />
  </div>
  <h2 v-show="posts.length == 0" style="color: red">
    Post list is empty
  </h2>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.title {
  margin-bottom: 15px;
}
</style>