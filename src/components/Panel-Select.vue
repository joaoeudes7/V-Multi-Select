<template>
  <div id="Panel">
    <div class="container-input">
      <input class="search" placeholder="Pesquisar..." v-model="textTyped">
    </div>
    <div class="list">
      <template v-for="(item, index) in filtedData">
        <span
          class="item-list"
          :key="index"
          @click="onSelect(item)"
        >{{ field ? item[field] : item }}</span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "Panel",
  props: {
    items: { type: Array, required: true },
    field: { type: String }
  },
  data: () => ({
    textTyped: ""
  }),
  methods: {
    getItems() {
      return this.filtedData;
    },
    onSelect(item) {
      this.$emit("select", item);
    }
  },
  computed: {
    filtedData() {
      let data = this.items;
      if (this.textTyped.trim()) {
        data = data.filter(item => {
          const _item = this.field ? item[this.field] : item;
          return _item.toLowerCase().includes(this.textTyped.toLowerCase());
        });
      }
      return data;
    }
  }
};
</script>

<style lang="scss" scoped>
#Panel {
  background: #f3f3f3;
  display: inline-block;
  width: 200px;
  padding: 4px;
  border-radius: 4px;
  border: 1px solid #d3d3d3;
  overflow: hidden;

  // Custom Scroll
  ::-webkit-scrollbar {
    width: 4px;
    background: #b1b1b14a;
  }

  ::-webkit-scrollbar-track {
    border-radius: 4px;
  }

  ::-webkit-scrollbar-thumb {
    border-radius: 4px;
    background: #d3d3d3;
  }
}

.search {
  width: 100%;
  border: none;
  border: 1px solid #d3d3d3;
  border-radius: 4px;
  box-sizing: border-box;
  padding: 6px 3px;
  margin-bottom: 5px;
}

.list {
  background: #fafafa;
  display: flex;
  height: 250px;
  flex-direction: column;
  border: 1px solid #d3d3d3;
  overflow-y: auto;
  border-radius: 4px;
}

.item-list {
  width: 100%;
  padding: 5px 0;
  text-align: center;
  border-bottom: 1px solid #d3d3d3;
  cursor: pointer;

  &:hover {
    background: #c5c5c54a;
  }
}

.empty {
  color: #3a3a3a;
}
</style>
