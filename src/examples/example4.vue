<template>

  <div id="sidebar">
    <Slider :title="curvepointName" :min="0" max="100" :step="1" :val="curvepointValue" @update="updateValue"></Slider>
  </div>

  <div id="viewer">
    <GeometryView :data="inputs" :path="path"></GeometryView>
  </div>
</template>

<script setup>
import { ref, onBeforeMount, computed } from "vue"
import GeometryView from "../components/MinimalisticGeometryView-MeshColors.vue"
import Slider from '../components/Slider.vue'
import Toggle from "../components/Toggle.vue"
import MetadataTextBox from "@/components/MetadataTextBox.vue"


//define path to grasshopper script
import def from "../assets/100hpdflat.gh"
const path = def

//define input names and values
const curvepointName = ref("curvePoint")
const curvepointValue = ref(1)

let metadata = ref([])

//define inputs
let inputs = ref({
  [curvepointName.value]: curvepointValue.value 
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

function receiveMetadata(newValue) {
  console.log("Metadata",newValue)
  metadata.value = newValue
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