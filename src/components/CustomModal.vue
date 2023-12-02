<script setup>
import PostForm from '@/components/PostForm.vue'

defineProps({
  isOpenModal: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['closeModal', 'create'])
function closeModal() {
  emit('closeModal', false)
}

function addPost(id) {
  emit('create', id)
}
</script>

<template>
  <div id="openModal" :class="isOpenModal ? 'open-popup white-popup' : 'white-popup'">
    <PostForm @create="addPost"></PostForm>
    <button title="Close (Esc)" type="button" class="btn-close" @click="closeModal">×</button>
  </div>
</template>

<style scoped>
.white-popup {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  z-index: 100;
  opacity: 0;
}

.open-popup {
  opacity: 1;
  transition: all 0.2s ease-in-out;
}

.btn-close {
  right: -35px;
  color: #fcfcfc;
  position: absolute;
  background: black;
  top: 0px;
  z-index: 9999;
  border: none;
  width: 35px;
  height: 35px;
  cursor: pointer;
}
</style>
