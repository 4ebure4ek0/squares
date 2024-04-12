<script setup>
defineProps({
    color: String
})

const emit = defineEmits(['deletePoint'])
</script>
<template>
    <span :style="{ background: color }" class="color_point" @click="emit('deletePoint', color)"></span>
</template>
<style>
.color_point {
  height: 18px;
  width: 18px;
  display: inline-block;
  cursor: pointer;
}
</style>