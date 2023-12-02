<script setup>
defineProps({
  page: {
    type: Number
  },
  limit: {
    type: Number
  },
  totalPages: {
    type: Number
  }
})

const emit = defineEmits(['pageNum'])
function changePage(pageNum) {
  emit('pageNum', pageNum)
}
</script>
<template>
  <ul class="page-nav">
    <li
      v-for="pageNum in totalPages"
      :key="pageNum"
      :class="{ 'current-page': page === pageNum }"
      @click="changePage(pageNum)"
    >
      {{ pageNum }}
    </li>
  </ul>
</template>
<style scoped>
.page-nav {
  list-style: none;
  display: flex;
  flex-direction: row;
}
.page-nav li {
  border: 1px solid #ccc;
  margin: 0 5px;
  padding: 10px 20px;
  cursor: pointer;
  transition: all 0.3s;
}
.page-nav li.current-page {
  background: #9c27b0;
  border: 1px solid #9c27b0;
  color: #fff;
}

.page-nav li:hover {
  background: #9c27b0;
  border: 1px solid #9c27b0;
  color: #fff;
  transition: all 0.3s;
}
</style>
