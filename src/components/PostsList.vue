<script setup>
import SinglePost from '@/components/SinglePost.vue'
defineProps({
  posts: {
    title: {
      type: String,
      required: true
    },
    body: {
      type: String,
      required: true
    }
  }
})

const emit = defineEmits(['delete'])
function deletePost(id) {
  emit('delete', id)
}
</script>

<template>
  <ul class="posts-list" v-if="posts.length > 0">
    <li v-for="post in posts" :key="post.id">
      <SinglePost :post="post" @delete="deletePost"></SinglePost>
    </li>
  </ul>
  <h3 v-else>You don't have any posts</h3>
</template>

<style scoped>
.posts-list {
  list-style: none;
  padding: 0;
}

.posts-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 10px auto;
  border: 1px solid #ddd;
  padding: 10px 20px;
  border-radius: 3px;
}

@media screen and (min-width: 768px) {
  .posts-list {
    min-width: 500px;
  }
}
</style>
