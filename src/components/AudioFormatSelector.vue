<template>
  <select v-model="selectedAudioFormat">
    <option v-for="audioFormat in audioFormats" :value="audioFormat" :key="audioFormat.id">
      {{ audioFormat.description }}
    </option>
  </select>
</template>

<script>
const constants = require("../constants");
export default {
  name: "AudioFormatSelector",
  data() {
    return {
      selectedAudioFormat: constants.audioFormats[0],
      audioFormats: constants.audioFormats,
    }
  }
}
</script>

<style scoped>

</style>