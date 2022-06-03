<template>
  <div>
    <h1>{{ likes }}</h1>
    <button @click="addLike">Add like</button>
    <h1>Page with posts</h1>
        <h1>{{$store.state.isAuth ? "Authorized" : "Need to authorize"}}</h1>
        <h1>{{$store.getters.doubleLikes}}</h1>
        <div>
          <my-button @click="$store.commit('incrementLikes')">Like</my-button>
          <my-button @click="$store.commit('decrementLikes')">Dislike</my-button>
        </div>
        <my-input
            v-model="searchQuery"
            placeholder="Search..."
            v-focus
        />
        <div class="app__btns">
          <my-button
          >
            Create post
          </my-button>
          <my-select
              v-model="selectedSort"
              :options="sortOptions"
          />
        </div>
        <my-dialog v-model:show="dialogVisible">
          <post-form
          />
        </my-dialog>
        <post-list
            :posts="sortedAndSearchedPosts"
            v-if="!isPostsLoading"
        />
        <div v-else>Loading...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/UI/MyDialog";
import MyInput from "@/components/UI/MyInput";
import {usePosts} from "@/hooks/usePosts";
import useSortedPosts from "@/hooks/useSortedPosts";
import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts";

export default {
  components: {
    MyInput,
    MyDialog,
    PostList,
    PostForm
  },
  data() {
    return {
      dialogVisible: false,
      sortOptions: [
        {value: 'title', name: 'by name'},
        {value: 'body', name: 'By content'}
      ]
    }
  },
  setup(props) {
    const {totalPages, isPostLoading, posts} = usePosts(10)
    const {sortedPosts, selectedSort} = useSortedPosts(posts)
    const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts)

    return {
      posts,
      sortedPosts,
      totalPages,
      sortedAndSearchedPosts,
      selectedSort,
      isPostLoading,
      searchQuery
    }
  }
}
</script>

<style>
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
}

.current-page {
  border: 2px solid teal;
}

.observer {
  height: 30px;
  background: green;
}
</style>
