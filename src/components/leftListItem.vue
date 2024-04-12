<script setup>
import { ref } from "vue";
import itemItem from "./itemItem.vue";

const open = ref(false);

const props = defineProps({
  title: String,
  list: Object,
});

const emit = defineEmits(["handleCheckList", "handleCheckItem"]);

const handleCheckItem = () => {
  return emit("handleCheckItem", props.title);
};
</script>
<template>
  <div class="list_item">
    <div class="list_head">
      <div
        @click="() => (open = !open)"
        class="arrow"
        :class="{ rotate: open }"
      >
        <svg
          width="27px"
          height="27px"
          stroke-width="2.3"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          color="#42567a"
        >
          <path
            d="M9 6L15 12L9 18"
            stroke="#42567a"
            stroke-width="2.3"
            stroke-linecap="round"
            stroke-linejoin="round"
          ></path>
        </svg>
      </div>
      <label class="list_title">
        <input
          type="checkbox"
          v-model="list.checked"
          @change="emit('handleCheckList', title)"
          :class="{ list_title_input: list.notFull }"
        />
        {{ title }}
      </label>
    </div>
    <div class="items" v-show="open">
      <itemItem
        v-for="(item, index) in Object.entries(list.items)"
        :title="item[0]"
        :item="item[1]"
        :key="index"
        v-on:handleCheckItem="handleCheckItem"
      />
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
  gap: var(--pad);
}

.list_title {
  font-size: 1.5em;
  font-weight: 500;
}

.list_title_input {
  position: relative;
}

.list_title_input::before {
  content: "";
  height: 7px;
  width: 7px;
  border-radius: var(--border-radius);
  background-color: var(--border-color);
  position: absolute;
  inset: 50%;
  transform: translate(-50%, -50%);
}

.arrow {
  cursor: pointer;
}

.arrow.rotate {
  transform: rotate(90deg);
}

.items {
  padding: var(--pad) 80px;
  display: flex;
  flex-direction: column;
  gap: var(--pad);
}
</style>
