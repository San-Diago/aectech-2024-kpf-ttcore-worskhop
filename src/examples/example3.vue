<template>

  <div id="sidebar">
    <Slider :title="vertoffsetSliderName" :min="0" max="1" :step="0.005" :val="vertoffsetSliderValue" @update="updateValue"></Slider>
    <Slider :title="horizoffsetSliderName" :min="0" max="1" :step="0.001" :val="horizoffsetValue" @update="updateValue"></Slider>
    <Slider :title="plywoodthicknessSliderName" :min="0" max="1" :step="0.01" :val="plywoodthicknessValue" @update="updateValue"></Slider>
  </div>

  <div id="viewer">
    <GeometryView :data="inputs" :path="path"></GeometryView>
  </div>
</template>

<script setup>
import { ref, onBeforeMount, computed } from "vue"
import GeometryView from "../components/MinimalisticGeometryView.vue"
import Slider from '../components/Slider.vue'
import Toggle from "../components/Toggle.vue"

//define path to grasshopper script
import def from "../assets/andoverTree.gh"
const path = def

//define input names and values
const vertoffsetSliderName = ref("VertOffset")
const vertoffsetSliderValue = ref(0.125)

const horizoffsetSliderName = ref("HorizOffset")
const horizoffsetValue = ref(0.125)

const plywoodthicknessSliderName = ref("PlywoodThickness")
const plywoodthicknessValue = ref(0.5)


//define inputs
let inputs = ref({
  [vertoffsetSliderName.value]: vertoffsetSliderValue.value ,
  [horizoffsetSliderName.value] : horizoffsetValue.value ,
  [plywoodthicknessSliderName.value] : plywoodthicknessValue.value

});

function updateValue(newValue, parameterName) {
  // Iterate over the inputs array
  for (const [key, value] of Object.entries(inputs.value)) {
    if (key == parameterName){
        inputs.value[key] = newValue
        console.log(parameterName + ':' + newValue)
    }
  }
}

</script>

<style scoped>

#sidebar {
  width: 310px;
  padding: 20px;
  flex-shrink: 0; 
}

#viewer { 
  width: 100%;
  margin: 20px
}

</style>