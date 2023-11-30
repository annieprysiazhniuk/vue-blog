<script>
import CustomButton from '@/components/CustomButton.vue'
export default {
  components: {
    CustomButton
  },
  data() {
    return {
      title: '',
      body: ''
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
    <div class="input-container">
      <label>Post title:</label>
      <input class="input" type="text" placeholder="Post title" v-model="title" />
    </div>
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

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

.input {
  padding: 5px 10px;
  min-height: 40px;
  border: 1px solid #828181;
  border-radius: 3px;
  font-family: monospace;
}

label {
  text-transform: uppercase;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 1px;
  margin-bottom: 5px;
  color: #333;
}
</style>
