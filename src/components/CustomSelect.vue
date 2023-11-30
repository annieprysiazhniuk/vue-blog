<script setup>
defineProps({
    modelValue: {
      type: String
  }, 
  options: {
    type: Array,
  }
})

const emit = defineEmits(['modelValue'])
function changeSelect(event) {
    emit('update:modelValue', event.target.value)
}
</script>

<template>

    <select name="post-sort" :value="modelValue" @change="changeSelect">
      <option value="">Sort by...</option>
      <option v-for="option in options" :key="option.value" :value="option.value">{{ option.name }}</option>
    </select>

</template>

<style scoped>
select {
    max-width: 200px;
    margin: 20px 0;
    min-height: 40px;
}
</style>