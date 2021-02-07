<template>
  <b-dropdown-item variant="dark" v-on:click="subItemClick">
    <div>
      {{ sub.Title }}
    </div>
  </b-dropdown-item>
</template>

<script>
export default {
  name: "GroupSubItem",
  props: ['sub'],
  methods: {
    subItemClick: function(){
      window.open(this.sub.WebsiteUrl, '_blank');
    }
  }
}
</script>

<style scoped>
  .text-black{
    color: black;
  }
  .foo{
    background: black;
  }
</style>