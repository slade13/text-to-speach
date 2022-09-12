<template>
  <select class="selectField" v-model="selectedLanguage" @change="updateVoice(); changeValue()">
    <option v-for="language in languages" :value="language" :key="language.id">
      {{ language.name }}
    </option>
  </select>
  <select class="selectField" v-model="selectedVoice" @change="changeValue">
    <option v-for="voice in selectedLanguage.voices" :value="voice" :key="voice.id">
      {{ voice.name }}
    </option>
  </select>

</template>

<script>
const constants = require("../constants");
export default {
  name: "LanguageSelector",
  props: ['defaultLanguage', 'defaultVoice'],
  emits: ['changeValue'],
  data() {
    return {
      selectedLanguage: this.defaultLanguage,
      selectedVoice: this.defaultVoice,
      languages: constants.languages,
    }
  },
  methods: {
    updateVoice() {
      this.selectedVoice = this.selectedLanguage.voices[0];
    },
    changeValue() {
      this.$emit('changeValue', this.selectedLanguage, this.selectedVoice);
      console.log('emit \'change-value\'')
    }
  }
}
</script>

<style scoped>

</style>