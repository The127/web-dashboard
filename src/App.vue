<template>
  <div id="app">
    <div class="d-flex justify-content-between">
      <h1>
        WebDashboard
      </h1>
      <b-input-group>
        <b-form-input class="myInput" v-on:click="searchBoxClick" placeholder="search groups..."/>
        <b-input-group-append>
          <b-button id="group-search" v-on:click="searchGroupButtonClick" class="search-button mr-1">
            <Magnify />
          </b-button>
          <b-tooltip target="group-search" triggers="hover">
            search groups
          </b-tooltip>
        </b-input-group-append>
      </b-input-group>
    </div>
    <div class="container">
      <ItemGroups/>
    </div>
  </div>
</template>

<script>
import Magnify from 'vue-material-design-icons/Magnify.vue';
import ItemGroups from "@/components/webdashboard/ItemGroups";

export default {
  name: 'App',
  components: {
    ItemGroups,
    Magnify
  },
  methods: {
    searchBoxClick: function (evt){
      evt.target.setSelectionRange(0, evt.target.value.length)
    },
    searchGroupButtonClick: function (){

    }
  }
}
</script>

<style>
  .myInput{
    background: transparent;
    -webkit-transition: background .2s linear;
    -ms-transition: background .2s linear;
    transition: background .2s linear;
    border: none;
    border-bottom: 1px solid gray;
    -webkit-box-shadow: none;
    box-shadow: none;
    border-radius: 0;
  }
  .myInput:focus{
    -webkit-box-shadow: none;
    box-shadow: none;
    border-bottom: 1px solid gray;
    box-shadow: none;
  }
  .search-button {
    border-radius: 0;
    border-style: none;
  }
</style>

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
