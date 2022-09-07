<template>
  <select v-model="selectedAudioCodec">
    <option v-for="audioCodec in audioCodecs" :value="audioCodec" :key="audioCodec.id">
      {{ audioCodec.id }}
    </option>
  </select>
</template>

<script>
const constants = require("../constants");
export default {
  name: "AudioCodecSelector",
  data() {
    return {
      selectedAudioCodec: constants.audioCodecs[0],
      audioCodecs: constants.audioCodecs,
    }
  }
}
</script>

<style scoped>

</style>