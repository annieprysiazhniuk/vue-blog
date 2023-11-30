<script>
import CustomModal from '@/components/CustomModal.vue'
import PostsList from '@/components/PostsList.vue'
import CustomTitle from '@/components/CustomTitle.vue'
import CustomButton from '@/components/CustomButton.vue'
export default {
  components: {
    CustomModal,
    PostsList,
    CustomTitle,
    CustomButton
  },
  data() {
    return {
      posts: [],
      isLoading: false,
      isOpenModal: false
    }
  },
  methods: {
    getPosts() {
      this.isLoading = true
      fetch('https://jsonplaceholder.typicode.com/posts?userId=10')
        .then((response) => response.json())
        .then((data) => {
          ;(this.posts = data), (this.isLoading = false)
        })
        .catch((error) => {
          console.error('Something went wrong: ', error)
        })
    },

    addPost(newPost) {
      this.posts.unshift(newPost);
      this.isOpenModal = false
    },

    deletePost(id) {
      this.posts = this.posts.filter((post) => post.id !== id)
    },

    openModal() {
      this.isOpenModal = !this.isOpenModal
    },

    closeModal() {
    this.isOpenModal = false
  }
  },
  created() {
    this.getPosts()
  },
}
</script>

<template>
  <p v-if="isLoading" class="loading">Loading...</p>
  <header>This is a header</header>
  <aside class="sidebar">
    <CustomTitle>Add a new post</CustomTitle>
    <CustomButton class="modal-button" @click="openModal">Add post</CustomButton>
    <CustomModal :isOpenModal="isOpenModal" @closeModal="closeModal" @create="addPost"></CustomModal>
  </aside>
  <main>
    <CustomTitle>List of posts</CustomTitle>
    <PostsList :posts="posts" :isOpenModal="isOpenModal" @delete="deletePost"></PostsList>
  </main>
</template>

<style scoped>
main {
  margin: 0 auto 50px 50px;
}
.loading {
  position: fixed;
  width: 100%;
  height: 100%;
  background: #fff;
  text-align: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.modal-button {
  width: 200px;
  min-height: 46px;
  font-weight: 600;
  text-transform: uppercase;
}
</style>
