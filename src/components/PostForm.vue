<script>
import CustomButton from '@/components/CustomButton.vue'
import CustomInput from './CustomInput.vue'
export default {
  components: {
    CustomButton,
    CustomInput,
  },
  data() {
    return {
      title: '',
      placeholder: 'Post title',
      body: '',
    }
  },
  methods: {
    addPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body
      }
      this.$emit('create', newPost)
      this.title = ''
      this.body = ''
    }
  }
}
</script>

<template>
  <form>
    <CustomInput v-model:title="title" :placeholder="placeholder"></CustomInput>
    <div class="input-container">
      <label>Post content:</label>
      <textarea class="input" type="text" placeholder="Post content" v-model="body"></textarea>
    </div>
    <CustomButton @click.prevent="addPost">Add post</CustomButton>
  </form>
</template>

<style scoped>
form {
  /* margin-bottom: 40px; */
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 3px;
}
</style>
