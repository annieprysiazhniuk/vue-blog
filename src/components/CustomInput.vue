<script setup>
defineProps({
  title: {
    type: String,
    required: true
  },
  placeholder: {
    type: String
  }
})

const emit = defineEmits(['update:title'])
function changeInput(event) {
  emit('update:title', event.target.value)
}
</script>

<template>
  <div class="input-container">
    <label>{{ placeholder }}:</label>
    <input
      class="input"
      type="text"
      :placeholder="placeholder"
      :value="title"
      @input="changeInput"
    />
  </div>
</template>

<style scoped></style>
