<script setup>
import { computed } from "vue";
import colorPoint from "./colorPoint.vue";

const props = defineProps({
  title: String,
  list: Object,
});

const emit = defineEmits(["changeIsSort", "deletePoint"]);

const itemColors = computed(() => {
  let itemPoints = [];
  Object.entries(props.list.items)
    .filter((item) => item[1].checked)
    .forEach((item) => {
      let points = [];
      for (let i = 0; i < item[1].quantity; i++) {
        points.push(item[1].color);
      }
      itemPoints.push(points);
    });
  if (props.list.isSorted) {
    return itemPoints.flat(Infinity).sort(() => Math.random() - 0.5);
  } else {
    return itemPoints;
  }
});

const deletePoint = (color) => {
  emit("deletePoint", [props.title, color]);
};
</script>
<template>
  <div class="list_item">
    <div class="list_head">
      <label class="list_title">
        {{ title }}
      </label>
      <button
        class="mix_btn"
        v-show="itemColors.length > 0"
        @click="emit('changeIsSort', title)"
      >
        {{ props.list.isSorted ? "Сортировать" : "Перемешать" }}
      </button>
    </div>
    <div
      class="items_sorted"
      v-if="list.isSorted"
      v-show="itemColors.length > 0"
    >
      <colorPoint
        v-for="color in itemColors"
        :color="color"
        v-on:deletePoint="deletePoint"
      />
    </div>
    <div class="items" v-else v-show="itemColors.length > 0">
      <div class="color_block" v-for="itemColor in itemColors">
        <colorPoint
          v-for="color in itemColor"
          :color="color"
          v-on:deletePoint="deletePoint"
        />
      </div>
    </div>
  </div>
</template>
<style scoped>
.list_item {
  border: 2px solid var(--border-color);
  padding: var(--pad);
  border-radius: var(--border-radius);
}

.list_head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: var(--pad);
}

.list_title {
  font-size: 1.5em;
  font-weight: 500;
}

.mix_btn {
  border: 2px solid var(--border-color);
  border-radius: var(--border-radius);
  background-color: var(--border-color);
  color: #fff;
  padding: var(--border-radius);
  cursor: pointer;
  font-weight: 500;
  transition: all 0.4s ease-in-out;
}

.mix_btn:hover {
  background: #fff;
  color: var(--border-color);
}

.items {
  padding: var(--pad) 80px;
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.items_sorted {
  padding: var(--pad) 80px;
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.color_block {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}
</style>
