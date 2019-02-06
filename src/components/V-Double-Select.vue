<template>
  <div id="V-Double-Select">
    <PanelSelect :field="field" :items="dataLeft" @select="selectLeft"/>
    <SwitchHelper @switchAll="switchAll"/>
    <PanelSelect :field="field" :items="dataRight" @select="selectRight"/>
  </div>
</template>

<script>
import PanelSelect from './Panel-Select';
import SwitchHelper from './SwitchHelper'

export default {
  name: "VDoubleSelect",
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
    selectLeft(item) {
      const indexOf = this.dataLeft.indexOf(item);
      this.dataLeft.splice(indexOf, 1);
      this.dataRight.push(item);
      this.onChange();
      this.onSelect(item);
    },
    selectRight(item) {
      const indexOf = this.dataRight.indexOf(item);
      this.dataRight.splice(indexOf, 1);
      this.dataLeft.push(item);
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
