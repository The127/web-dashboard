<template>
  <div class="my-3">
    <b-card>
    <div class="d-flex justify-content-between">
      <div>
        <h4>{{ group.Title }}</h4>
      </div>
      <b-button-toolbar>
        <b-input-group>
          <b-form-input class="myInput" v-on:click="searchBoxClick" placeholder="search items..."/>
          <b-input-group-append>
            <b-button :id="'group-search-' + group.Id" v-on:click="searchGroupButtonClick" class="search-button mr-1">
              <Magnify />
            </b-button>
            <b-tooltip :target="'group-search-' + group.Id" triggers="hover">
              search items in this group
            </b-tooltip>
          </b-input-group-append>
        </b-input-group>
        <b-button :id="'group-edit-' + group.Id" class="search-button mr-1">
          <Pencil />
        </b-button>
        <b-tooltip :target="'group-edit-' + group.Id" triggers="hover">
          edit this group
        </b-tooltip>
        <b-button :id="'group-add-' + group.Id" class="search-button">
          <Plus />
        </b-button>
        <b-tooltip :target="'group-add-' + group.Id" triggers="hover">
          add new item to this group
        </b-tooltip>
      </b-button-toolbar>
    </div>
    <b-container style="overflow-x: auto">
      <b-row class="flex-nowrap item-row">
        <GroupItem class="row-item zoom-item" v-for="item in items" :key="item.Id" :item="item" />
        <AddItem class="row-item" :group-id="group.Id" />
      </b-row>
    </b-container>
    </b-card>
  </div>
</template>

<script>
import GroupItem from "@/components/webdashboard/GroupItem";
import AddItem from "@/components/webdashboard/AddItem";
import Magnify from 'vue-material-design-icons/Magnify.vue';
import Pencil from 'vue-material-design-icons/Pencil.vue';
import Plus from 'vue-material-design-icons/Plus.vue';

export default {
  name: "ItemGroup",
  components: {
    AddItem,
    GroupItem,
    Magnify,
    Pencil,
    Plus,
  },
  data: function() {
    return {
      items: []
    }
  },
  props: ['group'],
  created() {
    const vm = this
    this.$axios.get('http://localhost:10000/itemgroups/' + vm.group.Id + '/items')
        .then(function (response) {
          vm.items = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
  },
  methods: {
    searchGroupButtonClick: function (){

    },
    searchBoxClick: function (evt){
      evt.target.setSelectionRange(0, evt.target.value.length)
    }
  }
}
</script>

<style scoped>
  .item-row {
    padding-top: 1em;
    padding-bottom: 1em;
    padding-left: 1em;
    padding-right: 1em;
  }
  .row-item {
    margin-left: 0.25em;
    margin-right: 0.25em;
    padding: 0;
  }
  .zoom-item {
    transition: transform .2s;
  }
  .zoom-item:hover {
    transform: scale(1.1);
    box-shadow: 0 0 0.5em rgba(0,0,0,0.3);
    z-index: 1000;
  }
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