<script setup>
import { ref } from "vue";
import leftListItem from "./components/leftListItem.vue";
import rightListItem from "./components/rightListItem.vue";

const lists = ref({
  list1: {
    items: {
      item1: {
        quantity: 23,
        color: "#FFC618",
        checked: false,
      },
      item2: {
        quantity: 19,
        color: "#FBCEB1",
        checked: false,
      },
      item3: {
        quantity: 7,
        color: "#B5B8B1",
        checked: false,
      },
      item4: {
        quantity: 3,
        color: "#7FFFD4",
        checked: false,
      },
      item5: {
        quantity: 21,
        color: "#78DBE2",
        checked: false,
      },
    },
    isSorted: false,
    checked: false,
    notFull: false,
  },
  list2: {
    items: {
      item1: {
        quantity: 2,
        color: "#E32636",
        checked: false,
      },
      item2: {
        quantity: 11,
        color: "#9966CC",
        checked: false,
      },
      item3: {
        quantity: 18,
        color: "#293133",
        checked: false,
      },
      item4: {
        quantity: 25,
        color: "#464451",
        checked: false,
      },
    },
    isSorted: false,
    checked: false,
    notFull: false,
  },
  list3: {
    items: {
      item1: {
        quantity: 4,
        color: "#2F4F4F",
        checked: false,
      },
      item2: {
        quantity: 5,
        color: "#A8E4A0",
        checked: false,
      },
      item3: {
        quantity: 16,
        color: "#47A76A",
        checked: false,
      },
      item4: {
        quantity: 43,
        color: "#62639B",
        checked: false,
      },
      item5: {
        quantity: 9,
        color: "#480607",
        checked: false,
      },
      item4: {
        quantity: 12,
        color: "#3E5F8A",
        checked: false,
      },
      item5: {
        quantity: 51,
        color: "#D5713F",
        checked: false,
      },
    },
    isSorted: false,
    checked: false,
    notFull: false,
  },
  list4: {
    items: {
      item1: {
        quantity: 36,
        color: "#9ACEEB",
        checked: false,
      },
      item2: {
        quantity: 33,
        color: "#DAD871",
        checked: false,
      },
      item3: {
        quantity: 17,
        color: "#414833",
        checked: false,
      },
      item4: {
        quantity: 26,
        color: "#256D7B",
        checked: false,
      },
    },
    isSorted: false,
    checked: false,
    notFull: false,
  },
  list5: {
    items: {
      item1: {
        quantity: 10,
        color: "#C9A0DC",
        checked: false,
      },
      item2: {
        quantity: 20,
        color: "#002F55",
        checked: false,
      },
      item3: {
        quantity: 30,
        color: "#E1CC4F",
        checked: false,
      },
      item4: {
        quantity: 40,
        color: "#006633",
        checked: false,
      },
      item5: {
        quantity: 50,
        color: "#5D76CB",
        checked: false,
      },
    },
    isSorted: true,
    checked: false,
    notFull: false,
  },
});

const handleCheckList = (listName) => {
  Object.values(lists.value[listName].items).forEach(
    (item) => (item.checked = lists.value[listName].checked)
  );
  lists.value[listName].notFull = false;
};

const handleCheckItem = (listName) => {
  const inappropriateArr = Object.values(lists.value[listName].items).filter(
    (item) => !item.checked
  );
  if (inappropriateArr.length > 0) {
    lists.value[listName].checked = false;
  } else {
    lists.value[listName].checked = true;
  }

  if (
    inappropriateArr.length ==
      Object.keys(lists.value[listName].items).length ||
    inappropriateArr.length == 0
  ) {
    lists.value[listName].notFull = false;
  } else {
    lists.value[listName].notFull = true;
  }
};

const changeIsSort = (listName) => {
  lists.value[listName].isSorted = !lists.value[listName].isSorted;
};

const deletePoint = ([listName, color]) => {
  Object.values(lists.value[listName].items).find((item) => item.color == color)
    .quantity--;
};
</script>

<template>
  <div class="container">
    <main>
      <section class="lists">
        <div class="side_bar">
          <div class="lists_list">
            <leftListItem
              v-for="(list, index) in Object.entries(lists)"
              :list="list[1]"
              :title="list[0]"
              :key="index"
              v-on:handleCheckList="handleCheckList"
              v-on:handleCheckItem="handleCheckItem"
            />
          </div>
        </div>
        <div class="side_bar">
          <div class="lists_list">
            <rightListItem
              v-for="(list, index) in Object.entries(lists)"
              :list="list[1]"
              :title="list[0]"
              :key="index"
              v-on:changeIsSort="changeIsSort"
              v-on:deletePoint="deletePoint"
            />
          </div>
        </div>
      </section>
    </main>
  </div>
</template>
<style>
.container {
  max-width: 1140px;
  margin: 0 auto;
  padding: 20px;
  height: 100vh;
}
main {
  height: 100%;
}
.lists {
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
.side_bar {
  border: 2px solid var(--border-color);
  padding: var(--pad);
  border-radius: var(--border-radius);
  height: 100%;
}
.lists_list {
  display: flex;
  flex-direction: column;
  gap: var(--pad);
}
</style>
