<template>
    <div class="col-6 text-left">
      <!--<a v-bind:href="'' + item.WebisteUrl" target="_blank">-->
        <b-card
            :title="item.Title"
            :img-src="item.ImageUrl"
            img-top
          >
          <div class="card-img-overlay d-flex justify-content-between">
            <div>
              <img :src="item.IconUrl" class="item-icon">
            </div>
            <div class="item-buttons d-flex justify-content-center">
              <Pencil fill-color="white" />
            </div>
          </div>
          <b-card-text>
            {{ item.Description }}
          </b-card-text>

        </b-card>
      <!--</a>-->
    </div>
</template>

<script>
import Pencil from 'vue-material-design-icons/Pencil.vue';

export default {
  name: "GroupItem",
  components: {
    Pencil
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
          console.log(response.data)
        })
        .catch(function (error) {
          console.log(error)
        })
  }
}
</script>

<style scoped>
  .item-icon {
    width: 2em;
    height: 2em;
  }
  .item-buttons {
    height: 2em;
    background: black;
  }
</style>