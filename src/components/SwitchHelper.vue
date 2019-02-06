<template>
  <div class="switch">
    <button class="button">
      <span class="icon" @click="switchAll" v-html="icons.switchIcon"/>
    </button>
  </div>
</template>

<script>
import _icons from './_icons.js';

export default {
  name: 'SwitchHelper',
  data: () => ({
    icons: _icons
  }),
  methods: {
    switchAll() {
      this.$emit('switchAll')
    }
  }
};
</script>

<style lang="scss" scoped>
.switch {
  display: flex;
  flex-direction: column;
  margin: 5px;

  .icon {
    fill: #656464;
  }
}

.button {
  background: none;
  width: 40px;
  height: 40px;
  padding: 5px;
  border-radius: 50%;
  border: none;
  cursor: pointer;

  &:hover {
    background: #6666664a
  }
}
</style>
