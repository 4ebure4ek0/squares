<script setup>
defineProps({
  title: String,
  item: Object,
});

const emit = defineEmits(["handleCheckItem"]);
</script>
<template>
  <div class="color_item">
    <label>
      <input
        type="checkbox"
        v-model="item.checked"
        @change="emit('handleCheckItem')"
      />
      {{ title }}
    </label>
    <div class="values">
      <input type="number" v-model="item.quantity" min="0" />
      <input type="color" v-model="item.color" />
    </div>
  </div>
</template>
<style>
.color_item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.values {
  display: flex;
  gap: 10px;
}
</style>
