<template>
  <label class="select" for="audioFormatSelect">Select audio format</label>
  <select class="selectField" id="audioFormatSelect" v-model="selectedAudioFormat" @change="changeValue">
    <option v-for="audioFormat in audioFormats" :value="audioFormat" :key="audioFormat.id">
      {{ audioFormat.description }}
    </option>
  </select>
</template>

<script>
const constants = require("../constants");
export default {
  name: "AudioFormatSelector",
  props: ['defaultFormat'],
  emits: ['changeValue'],
  data() {
    return {
      selectedAudioFormat: this.defaultFormat,
      audioFormats: constants.audioFormats,
    }
  },
  methods: {
    changeValue() {
      this.$emit('changeValue', this.selectedAudioFormat);
      console.log('emit \'change-value\'')
    }
  }
}
</script>

<style scoped>

</style>