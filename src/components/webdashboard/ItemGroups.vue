<template>
  <div>
    oof
    <div v-for="group in groups" :key="group.Id">
      blubb
      <p>{{ group.Id }}</p>
      <GroupItem group="foo"></GroupItem>
    </div>
  </div>
</template>

<script>
import GroupItem from "@/components/webdashboard/GroupItem";
export default {
  components: {GroupItem}
}
</script>
<script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script>

<script>
export default {
  name: "ItemGroups",
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
          console.log(response.data)
        })
        .catch(function (error) {
          console.log(error)
        })
  }
}
</script>

<style scoped>

</style>