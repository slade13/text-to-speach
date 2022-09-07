<template>
  <select v-model="selectedLanguage">
    <option v-for="language in languages" :value="language" :key="language.id">
      {{ language.name }}
    </option>
  </select>
  <select v-model="selectedVoice">
    <option v-for="voice in selectedLanguage.voices" :value="voice" :key="voice.id">
      {{ voice.name }}
    </option>
  </select>

</template>

<script>
const constants = require("../constants");
export default {
  name: "LanguageSelector",
  data() {
    return {
      selectedLanguage: constants.languages[0],
      selectedVoice: constants.languages[0].voices[0],
      languages: constants.languages,
    }
  },
  watch: {
    selectedLanguage(newValue) {
      this.selectedVoice = newValue.voices[0];
    }
  }
}
</script>

<style scoped>

</style>