<template>
  <div id="app">
    <div class="d-flex justify-content-center">
      <h1>
        WebDashboard
      </h1>
    </div>
    <div class="container">
      <ItemGroups/>
    </div>
  </div>
</template>

<script>
import ItemGroups from "@/components/webdashboard/ItemGroups";

export default {
  name: 'App',
  components: {
    ItemGroups,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
