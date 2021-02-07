<template>
    <div class="col-sm-12 col-md-6 col-xl-4 text-left">
      <b-card :img-src="item.ImageUrl" no-body>
        <div class="card-img-overlay d-flex flex-column justify-content-between">
          <div class="d-flex justify-content-between">
            <a class="item-icon" :href="item.WebisteUrl" target="_blank">
              <img :id="'item-icon-' + item.Id"  :src="item.IconUrl" class="item-icon">
            </a>
            <b-tooltip :target="'item-icon-' + item.Id" triggers="hover">
              {{ item.WebisteUrl }}
            </b-tooltip>
            <div class="d-flex flex-row">
              <div class="col item-button d-flex justify-content-center mr-1"
                v-on:click="deleteItem">
                <div :id="'item-edit-' + item.Id" class="align-self-center">
                  <Pencil fill-color="white" />
                </div>
                <b-tooltip :target="'item-edit-' + item.Id" triggers="hover">
                  edit item
                </b-tooltip>
              </div>
              <div class="item-button d-flex justify-content-center mr-1">
                <div :id="'item-delete-' + item.Id" class="align-self-center">
                  <Delete fill-color="white" />
                </div>
                <b-tooltip :target="'item-delete-' + item.Id" triggers="hover">
                  delete item
                </b-tooltip>
              </div>
              <div v-if="subitems && subitems.length > 0" class="item-button d-flex justify-content-center mr-1">
                <b-dropdown class="sub-dropdown" variant="link" right :id="'item-sub-' + item.Id" toggle-class="w-100 text-decoration-none" no-caret>
                  <template #button-content>
                    <div class="w-100 h-100 d-flex justify-content-center">
                      <div class="align-self-center text-white">
                        <ChevronDown />
                      </div>
                    </div>
                  </template>
                  <GroupSubItem v-for="sub in subitems" :key="sub.Id" :sub="sub"/>
                </b-dropdown>
                <b-tooltip :target="'item-sub-' + item.Id" triggers="hover">
                  toggle sub items
                </b-tooltip>
              </div>
              <div class="item-button d-flex justify-content-center">
                <a :id="'item-open-' + item.Id" class="align-self-center" :href="item.WebisteUrl" target="_blank">
                  <OpenInNew fill-color="white" />
                </a>
                <b-tooltip :target="'item-open-' + item.Id" triggers="hover">
                  {{ item.WebisteUrl }}
                </b-tooltip>
              </div>
            </div>
          </div>
          <a :href="item.WebisteUrl" target="_blank" class="overlay-dark text-white">
            <b-card-title>
              {{ item.Title }}
            </b-card-title>
            <b-card-text>
              {{ item.Description }}
            </b-card-text>
          </a>
        </div>
      </b-card>
    </div>
</template>

<script>
import Pencil from 'vue-material-design-icons/Pencil.vue';
import Delete from 'vue-material-design-icons/Delete.vue';
import OpenInNew from 'vue-material-design-icons/OpenInNew.vue';
import ChevronDown from 'vue-material-design-icons/ChevronDown.vue';
import GroupSubItem from "@/components/webdashboard/GroupSubItem";

export default {
  name: "GroupItem",
  components: {
    GroupSubItem,
    Pencil,
    Delete,
    OpenInNew,
    ChevronDown
  },
  data: function(){
    return {
      subitems: []
    }
  },
  props: ['item'],
  created() {
    const vm = this
    this.$axios.get('http://localhost:10000/items/' + vm.item.Id + '/subitems')
        .then(function (response) {
          vm.subitems = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
  },
  methods:{
    deleteItem() {
      console.log("foo")
    }
  }
}
</script>

<style scoped>
  .item-icon {
    width: 2em;
    height: 2em;
  }
  .item-button {
    cursor: pointer;
    height: 2em;
    width: 2em;
    background: rgba(255, 255, 255, 0.2);
    transition: all .2s;
  }
  .item-button:hover {
    background: rgba(255, 255, 255, 0.5);
    color: black;
  }
  .overlay-dark{
    background: rgba(0, 0, 0, 0.5);
    margin-right: -20px;
    margin-left: -20px;
    margin-bottom: -20px;
    padding: 20px;
  }
  .sub-dropdown {
    width: 2em;
    height: 2em;
  }
  .foo{

  }
</style>