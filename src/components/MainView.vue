<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Enter the text below:
    </p>
    <LanguageSelector />
    <AudioCodecSelector />
    <AudioFormatSelector />
    <SpeechRateSelector />
    <textarea id="textToSpeech" v-model="tts"></textarea>
    <button @click="submitText">Submit</button>
    <audio controls :class="{hide : hidePlayer}" ref="audioPlayer">
      <source :src="returnedAudio" type="audio/mp3" />
    </audio>
  </div>
</template>

<script>
import LanguageSelector from "@/components/LanguageSelector";
import AudioCodecSelector from "@/components/AudioCodecSelector";
import AudioFormatSelector from "@/components/AudioFormatSelector";
import SpeechRateSelector from "@/components/SpeechRateSelector";

const axios = require("axios");
const config = require("../config.js");

export default {
  name: 'MainView',
  components: {
    LanguageSelector,
    AudioCodecSelector,
    AudioFormatSelector,
    SpeechRateSelector
  },
  props: {
    msg: String
  },
  data() {
    return {
      tts: "",
      hidePlayer: true,
      returnedAudio: "data:audio/mpeg;base64,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qqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqkxBTUUzLjk5LjWqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqr/4xjExAAAA0gAAAAAqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqo="
    }
  },
  methods: {
    submitText() {
      const encodedParams = new URLSearchParams();
      encodedParams.append("src", this.tts);
      encodedParams.append("hl", "en-us");
      encodedParams.append("r", "0");
      encodedParams.append("c", "mp3");
      encodedParams.append("f", "8khz_8bit_mono");
      encodedParams.append("b64", "true");

      let vm = this;

      const options = {
        method: 'POST',
        url: 'https://api.voicerss.org/',
        params: {key: config.VOICERSS_API_KEY},
        headers: {
          'content-type': 'application/x-www-form-urlencoded',
        },
        data: encodedParams
      };
      axios.request(options).then((response) => {
        console.log(response.data);
        vm.returnedAudio = response.data;
        vm.$refs.audioPlayer.load();
        vm.hidePlayer = false;
        vm.$refs.audioPlayer.play();
      }).catch((error) => {
        console.error(error);
        vm.hidePlayer = true;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#textToSpeech {
  width: 500px;
  height: 150px;
}

button {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hide {
  display: none;
}
</style>
