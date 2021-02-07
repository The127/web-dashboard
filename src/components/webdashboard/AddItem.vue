<template>
  <div class="col-sm-12 col-md-6 col-xl-4 text-left">
    <!--<a v-bind:href="'' + item.WebisteUrl" target="_blank">-->
    <b-card class="h-100 bg-light">
      <div class="card-img-overlay d-flex justify-content-center">
        <div :id="'item-add-' + groupId" class="zoom-item add-button align-self-center d-flex justify-content-center"
            v-on:click="addButtonClick">
          <Plus class="icon-2x align-self-center" fill-color="white"/>
        </div>
        <b-tooltip :target="'item-add-' + groupId" triggers="hover">
          add new item
        </b-tooltip>
      </div>
    </b-card>
    <!--</a>-->
  </div>
</template>

<script>
import Plus from 'vue-material-design-icons/Plus.vue';

export default {
  name: "AddItem",
  components: {
    Plus,
  },
  props: {
    groupId: String
  },
  methods: {
    addButtonClick: function (){

    }
  }
}
</script>

<style scoped>
  .add-button {
    width: 6em;
    height: 6em;
    border-radius: 3em;
    background: gray;
    cursor: pointer;
  }

  .material-design-icon.icon-2x {
    height: 4em;
    width: 4em;
  }

  .material-design-icon.icon-2x > .material-design-icon__svg {
    height: 4em;
    width: 4em;
  }

  .zoom-item {
    transition: transform .2s;
    z-index: 1;
  }
  .zoom-item:hover {
    transform: scale(1.1);
    box-shadow: 0 0 1em rgba(0,0,0,0.3);
    z-index: 1000;
  }
</style>