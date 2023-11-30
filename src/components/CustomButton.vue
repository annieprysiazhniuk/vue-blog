<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<style scoped>
.btn {
  padding: 10px 20px;
  border: 1px solid #9c27b0;
  color: #9c27b0;
  border-radius: 3px;
  background: #fff;
  cursor: pointer;
  transition: all 0.3s;
}

.btn:hover {
  background: #9c27b0;
  color: #fff;
  transition: all 0.3s;
}
</style>
