<script setup>
import CustomButton from '@/components/CustomButton.vue'

defineProps({
  post: {
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
  <div>
    <h4><strong>Title:</strong> {{ post.title }}</h4>
    <p><strong>Description:</strong> {{ post.body }}</p>
  </div>
  <div class="actions-container">
    <CustomButton @click="deletePost(post.id)" class="btn-delete">Delete</CustomButton>
    <CustomButton class="btn-edit">Edit</CustomButton>
  </div>
</template>

<style scoped>
strong {
  font-weight: 600;
}
.btn {
  margin-left: 20px;
  min-width: 85px;
}
.btn-delete {
    margin-bottom: 5px;
}
.actions-container {
    display: flex;
    align-items: flex-end;
    flex-direction: column;
}
</style>
