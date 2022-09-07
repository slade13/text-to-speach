<template>
  <div class="sliderContainer">
    <input type="range" min="-10" max="10" value="0" class="slider" id="myRange">
  </div>
</template>

<script>
export default {
  name: "SpeechRateSelector",
  data() {
    return {

    }
  }
}
</script>

<style scoped>
.sliderContainer {
  margin: 7px 0;
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
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: #04AA6D;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: #04AA6D;
  cursor: pointer;
}
</style>