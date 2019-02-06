<template>
  <div id="app">
    <VDoubleSelect
      ref="DoubleSelect"
      :left="arrayExample"
      :right="arrayEmpty"
      @change="showData"
      @select="showSelected"
    />
  </div>
</template>

<script>
import VDoubleSelect from "./components/V-Multi-Select";

export default {
  name: "app",
  components: {
    VDoubleSelect
  },
  data: () => ({
    arrayExample: [],
    arrayEmpty: []
  }),
  mounted() {
    for (let index = 0; index < 16; index++) {
      this.arrayExample.push(`Hi ${index}`);
    }
  },
  methods: {
    showData(data) {
      console.group('New Change:', data);
    },
    getDataLeft() {
      console.log(this.$refs.DoubleSelect.dataLeft);
    },
    getDataRight() {
      console.log(this.$refs.DoubleSelect.dataRight);
    },
    showSelected(data) {
      console.log(`New Selected: ${data}`);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
