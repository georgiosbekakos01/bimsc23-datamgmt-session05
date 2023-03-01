<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
    // Import other Vue components in order to add them to a template.
    import SliderInput from "./components/SliderInput.vue";
    import ToggleInput from "./components/ToggleInput.vue";
    import GeometryView from "./components/GeometryView.vue";

    // Imports from packages

    // Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
    // When ref attribute is added to element, this element then can be referenced
    // in template. It is sort of templatecement of getElementById (but better)
    import { ref } from "vue";

    // Define variables and constants

    var slider1 = ref(15);
    var slider2 = ref(32);
    var slider3 = ref(15);
    var slider4 = ref(0);
    var slider5 = ref(Math.PI*2);
    var slider6 = ref(0);
    var slider7 = ref(Math.PI);
    var runToggle = ref(true);


    function updateValue(newValue, parameterName) {
      if (parameterName === "radius") {
        slider1.value = newValue;
        console.log(newValue)
      }
      if (parameterName === "widthSegments") {
        slider2.value = newValue;
      }
      if (parameterName === "heightSegments") {
        slider3.value = newValue;
      }
      if (parameterName === "phiStart") {
        slider4.value = newValue;
      }
      if (parameterName === "phiLegth") {
        slider5.value = newValue;
      }
      if (parameterName === "thetaStart") {
        slider6.value = newValue;
      }
      if (parameterName === "thetaLength") {
        slider7.value = newValue;
      }
    }




    function updateToggle(newValue) {
      runToggle.value = newValue;
    }






</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
    <div id="top-bar">
      <div id="title-container">
        <img class="logo-image" alt="Iaac logo" src="./assets/download.png" style="transform: scale(0.6)" />

        <h2>Digital Tools for Cloud-based Data Management</h2>
      </div>
    </div>

    <div id="content">
      <!-- First example -> button -->
      <!-- <button @click="increment">Add one more</button>
      <p>Count is: {{  count }}</p> -->
      <div class="titlebar">
        <!-- Vue component injected into App.vue component template.
        That makes it App.vue a parent and SliderInput.vue a child. -->
          <SliderInput title="radius"
          v-bind:min="0" v-bind:max="20" v-bind:step="0.1"
          v-on:updateValue="updateValue"/>

          <SliderInput title="widthSegments"
          v-bind:min="3" v-bind:max="60" v-bind:step="1"
          v-on:updateValue="updateValue"/>

          <SliderInput title="heightSegments"
          v-bind:min="2" v-bind:max="30" v-bind:step="1"
          v-on:updateValue="updateValue"/>

          <SliderInput title="phiStart"
          v-bind:min="0" v-bind:max="6" v-bind:step="0.1"
          v-on:updateValue="updateValue"/>

          <SliderInput title="phiLength"
          v-bind:min="0" v-bind:max="6" v-bind:step="0.1"
          v-on:updateValue="updateValue"/>

          <SliderInput title="thetaStart"
          v-bind:min="0" v-bind:max="6" v-bind:step="0.1"
          v-on:updateValue="updateValue"/> 

          <SliderInput title="thetaLength"
          v-bind:min="0" v-bind:max="6" v-bind:step="0.1"
          v-on:updateValue="updateValue"/>


          <ToggleInput title="Skeleton" 
          v-on:updateValue="updateToggle">
          </ToggleInput>

          




        <!--<h2>Value received in App.vue: {{ slider1 }}</h2>
        <h2>Value received in App.vue: {{ runToggle }}</h2>-->
      </div>

      <div id="content">
        <GeometryView :radius="slider1" :widthSegments="slider2" :heightSegments="slider3" :phiStart="slider4" :phiLength="slider5" :thetaStart="slider6" :thetaLength="slider7" :meshBoolean="runToggle" />

        <!-- uncomment to add another geometryview -->
        <!-- <GeometryView :size="firstSlider"/> -->
      </div>
    </div>
</template>

<!-- Style is for CSS styling -->
<style>
    #app {
      font-family: 'Courier New', Courier, monospace;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      color: rgb(255, 255, 255);
    }

    #top-bar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      /*background-color: rgb(0, 0, 0);*/
    }

    #title-container {
      display: flex;
      align-items: center;
      color: white;
      margin-right: 1.5rem;
    }

    #content {
      display: flex;
    }

    .logo-image {
      height: 3.25rem;
      padding: 0.5rem;
    }
    body {
      background: rgb(255, 255, 255);
    }
    h2 {
      font-size: 1.125rem;
      font-weight: 600;
      letter-spacing: -0.05em;
      font-size: 1.125rem;
      font-weight: 600;
      letter-spacing: 0.01em;
    }
</style>