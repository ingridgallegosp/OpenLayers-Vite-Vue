<template>
  <div id="app">
    <div class="cell cell-map">
      <MapContainer></MapContainer>
    </div>
    <div class="cell cell-edit">Edit</div>
    <div class="cell cell-inspect">Inspect</div>
  </div>
</template>

<script setup>
import MapContainer from "./components/MapContainer.vue";
</script>

<script>
export default {
  name: "App",
};
</script>

<style>
* {
  margin: 0;
}
html,
body {
  height: 100vh;
  width: 100vw;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 100vh;
  display: grid;
  grid-auto-rows: 1fr;
  grid-gap: 1rem;
  padding: 1rem;
  box-sizing: border-box;
}

.cell {
  border-radius: 4px;
  background-color: lightgrey;
}

.cell-map {
  grid-column: 1;
  grid-row-start: 1;
  grid-row-end: 3;
}

.cell-edit {
  grid-column: 2;
  grid-row: 1;
}

.cell-inspect {
  grid-column: 2;
  grid-row: 2;
}
</style>
