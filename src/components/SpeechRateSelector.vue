<template>
  <div class="sliderContainer">
    <label class="speed" for="myRange">Speed</label>
    <input type="range" min="-10" max="10" v-model="speed" @input="changeValue" class="slider" id="myRange">
  </div>
</template>

<script>
export default {
  name: "SpeechRateSelector",
  props: ['defaultSpeed'],
  emits: ['changeValue'],
  data() {
    return {
        speed: this.defaultSpeed,
    }
  },
  methods: {
    changeValue() {
      this.$emit('changeValue', this.speed);
      console.log('emit \'change-value\'')
    }
  }
}
</script>

<style scoped>
.sliderContainer {
  margin: 30px 100px;
}
.slider {
  -webkit-appearance: none;
  width: 500px;
  height: 15px;
  border-radius: 5px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #04AA6D;
  cursor: pointer;
}

</style>