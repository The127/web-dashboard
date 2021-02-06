<template>
  <div>
    <div v-for="group in groups" :key="group.Id">
        <ItemGroup v-bind:group="group"></ItemGroup>
    </div>
  </div>
</template>

<script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>

<script>
import ItemGroup from "@/components/webdashboard/ItemGroup";

export default {
  name: "ItemGroups",
  components: {ItemGroup},
  data: function(){
    return {
      greeting: 'oi cunt ass',
      groups: []
    }
  },
  created(){
    var vm = this
    this.$axios.get('http://localhost:10000/itemgroups')
        .then(function (response) {
          vm.groups = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
  }
}
</script>

<style scoped>

</style>