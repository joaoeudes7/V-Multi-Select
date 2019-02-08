<template>
  <div id="V-Double-Select">
    <PanelSelect :field="field" :items="dataLeft" @select="selectLeft"/>
    <SwitchHelper @switchAll="switchAll" @moveLeft="moveAllLeft" @moveRight="moveAllRight"/>
    <PanelSelect :field="field" :items="dataRight" @select="selectRight"/>
  </div>
</template>

<script>
import PanelSelect from './Panel-Select';
import SwitchHelper from './SwitchHelper'

export default {
  name: 'VMultiSelect',
  components: {
    PanelSelect,
    SwitchHelper
  },
  props: {
    left: { type: Array, required: true },
    right: { type: Array, required: true },
    field: { type: String }
  },
  data: () => ({
    dataLeft: [],
    dataRight: []
  }),
  mounted() {
    this.dataLeft = this.left;
    this.dataRight = this.right;
  },
  methods: {
    removeItemArray(array, item) {
      const indexOf = array.indexOf(item);
      array.splice(indexOf, 1);
    },
    selectLeft(item) {
      this.removeItemArray(this.dataLeft, item);
      this.dataRight = [...this.dataRight, item];
      this.onChange();
      this.onSelect(item);
    },
    selectRight(item) {
      this.removeItemArray(this.dataRight, item);
      this.dataLeft = [...this.dataLeft, item];
      this.onChange();
      this.onSelect(item);
    },
    onSelect(item) {
      this.$emit('select', item)
    },
    switchAll() {
      const aux = this.dataLeft.slice();
      this.dataLeft = this.dataRight.slice()
      this.dataRight = aux.slice();
      this.onChange();
    },
    moveAllRight() {
      this.dataLeft = [...new Set([...this.dataLeft, ...this.dataRight])]
      this.dataRight = []
      this.onChange()
    },
    moveAllLeft() {
      this.dataRight = [...new Set([...this.dataLeft, ...this.dataRight])]
      this.dataLeft = []
      this.onChange()
    },
    onChange() {
      const changeReport = {
        'left': this.dataLeft,
        'right': this.dataRight
      }
      this.$emit('change', changeReport);
    }
  }
};
</script>

<style lang="scss" scoped>
#V-Double-Select {
  display: inline-flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: center;
  border-radius: 4px;
  padding: 4px;
  user-select: none;
}
</style>
