<template>
    <div class="col-6">
      {{ item.WebisteUrl }}
      <b-card
          style="border-radius: 100px"
          overlay
          :img-src="item.ImageUrl">
        <div class="card-img-overlay text-white">
          <div class="row justify-content-start overlay-dark py-3" style="margin-left: -20px; margin-right: -20px">
            <div class="col-12 text-white text-left">
              <a v-bind:href="'' + item.WebisteUrl" target="_blank">
                {{ item.Title }}
              </a>
            </div>
            <div class="col-12 text-left text-muted">
              {{ item.Description }}
            </div>
          </div>
        </div>
      </b-card>
    </div>
</template>

<script>
export default {
  name: "GroupItem",
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

.overlay-dark {
  background-color: rgba(0, 0, 0, 0.5);
}
</style>