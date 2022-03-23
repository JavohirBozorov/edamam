<template>
  <div id="app">
    <div class="spinner">
      <!-- <SpinnerComponent /> -->
    </div>
    <MealList />
  </div>
</template>

<script>
import MealList from "./components/MealList.vue";
// import SpinnerComponent from "./components/SpinnerComponent.vue";

export default {
  name: "App",
  components: {
    MealList,
    // SpinnerComponent,
  },
};
</script>

<style>
template,
html,
h1,
body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
h1 {
  color: #0d0d0d;
  padding-top: 1rem;
  text-align: center;
}
#app {
  background-color: #fef9f8;
  min-height: 100vh;
}
.spinner {
  position: relative;
  align-items: center;
  z-index: 5;
}
</style>
