<template>
  <div>
  <div class="d-flex">
    {{ group.Title }}
  </div>
  <b-container style="overflow-x: auto">
  <b-row class="flex-nowrap">
    <GroupItem v-for="item in items" :key="item.Id" v-bind:item="item" />
  </b-row>
  </b-container>
  </div>
</template>

<script>
import GroupItem from "@/components/webdashboard/GroupItem";
export default {
  name: "ItemGroup",
  components: {GroupItem},
  data: function() {
    return {
      items: []
    }
  },
  props: ['group'],
  created() {
    const vm = this
    this.$axios.get('http://webdashboardapi.docker.the127.de/itemgroups/' + vm.group.Id + '/items')
        .then(function (response) {
          vm.items = response.data
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