<script setup>
import { ref } from "vue";
// Define properties that you will be able to access from parent component. 
// Those properties will be binded from parent to child. 
// Available JavaScript types: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
const props = defineProps(['title', 'min', 'max', 'step'])

const title_b = ref(props.title)
// Define events that will be accessible from parent component
const emits = defineEmits(['updateValue'])


var sliderValue = ref(Math.PI)

function sendValueUpate(){
  emits('updateValue', sliderValue.value, title_b.value)
  console.log('sliderValue')
}


</script>

<template>
<div>
	<form class="definition-input">
			<label class="input-title" for="range-slider">{{ title }}: {{ sliderValue }}</label>

			<input type="range" class="slide"
			v-bind:min="min" v-bind:max="max" v-bind:step="step"
			v-model="sliderValue" 
      v-on:input="sendValueUpate"
			/>
	</form>
</div>


</template>

<style scoped>
.slide {
  width: 95%;
  background:(rgb(0, 0, 0));
  height: 30px;
  border-radius: 10px;
  margin: 5px 0px;
}
</style>



