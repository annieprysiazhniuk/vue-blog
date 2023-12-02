<script>
import axios from 'axios'
import CustomModal from '@/components/CustomModal.vue'
import PostsList from '@/components/PostsList.vue'
import CustomTitle from '@/components/CustomTitle.vue'
import CustomButton from '@/components/CustomButton.vue'
import CustomSelect from '@/components/CustomSelect.vue'
import CustomInput from '@/components/CustomInput.vue'
import PostPagination from '@/components/PostPagination.vue'
export default {
  components: {
    CustomModal,
    PostsList,
    CustomTitle,
    CustomButton,
    CustomSelect,
    CustomInput,
    PostPagination
  },
  data() {
    return {
      posts: [],
      isLoading: false,
      isOpenModal: false,
      page: 1,
      limit: 10,
      totalPages: 0,
      modelValue: '',
      sortOptions: [
        { value: 'title', name: 'Post title' },
        { value: 'body', name: 'Post message' }
      ],
      searchQuery: ''
    }
  },
  methods: {
    async getPosts() {
      this.isLoading = true
      try {
        const response = await axios(`https://jsonplaceholder.typicode.com/posts`, {
          params: {
            _limit: this.limit,
            _page: this.page
          }
        })
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.posts = response.data
        this.isLoading = false
      } catch (error) {
        console.error('Something went wrong: ', error)
      }
    },

    addPost(newPost) {
      this.posts.unshift(newPost)
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
    },

    getPostsPage(page) {
      this.page = page
      this.getPosts()
    }
  },
  created() {
    this.getPosts()
  },

  watch: {
    modelValue(choosenSortOpt) {
      this.posts.sort((post1, post2) => {
        return post1[choosenSortOpt]?.localeCompare(post2[choosenSortOpt])
      })
    }
  },

  computed: {
    searchedPosts() {
      return this.posts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      )
    }
  }
}
</script>

<template>
  <p v-if="isLoading" class="loading">Loading...</p>
  <header>This is a header</header>
  <aside class="sidebar">
    <CustomTitle>Add a new post</CustomTitle>
    <CustomButton class="modal-button" @click="openModal">Add post</CustomButton>
    <CustomSelect :options="sortOptions" v-model="modelValue"></CustomSelect>
    <CustomInput v-model:title="searchQuery" placeholder="Search..." class="search"></CustomInput>
    <CustomModal
      :isOpenModal="isOpenModal"
      @closeModal="closeModal"
      @create="addPost"
    ></CustomModal>
  </aside>
  <main>
    <CustomTitle>List of posts</CustomTitle>
    <PostsList :posts="searchedPosts" :isOpenModal="isOpenModal" @delete="deletePost"></PostsList>
    <PostPagination
      :totalPages="totalPages"
      :page="page"
      :limit="limit"
      @pageNum="getPostsPage"
    ></PostPagination>
  </main>
</template>

<style scoped>
main {
  margin: 0 auto 50px 50px;
}

aside {
  display: flex;
  flex-direction: column;
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
  width: 250px;
  min-height: 46px;
  font-weight: 600;
  text-transform: uppercase;
}

.search {
  max-width: 250px;
}
</style>
