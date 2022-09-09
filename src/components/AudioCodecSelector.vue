<template>
  <select v-model="selectedAudioCodec" @change="changeValue">
    <option v-for="audioCodec in audioCodecs" :value="audioCodec" :key="audioCodec.id">
      {{ audioCodec.id }}
    </option>
  </select>
</template>

<script>
const constants = require("../constants");
export default {
  name: "AudioCodecSelector",
  props: ['defaultCodec'],
  emits: ['changeValue'],
  data() {
    return {
      selectedAudioCodec: this.defaultCodec,
      audioCodecs: constants.audioCodecs,
    }
  },
  methods: {
    changeValue() {
      this.$emit('changeValue', this.selectedAudioCodec);
      console.log('emit \'change-value\'')
    }
  }
}
</script>

<style scoped>

</style>