<template>
  <div id="app">
    <div v-for="(item,i) in items" :key ='i'>
      <list-item :item="item" class="item" v-on:itemChanged="$emit('realoadList')"></list-item>
    </div>
  </div>
</template>

<script>
import ListItem from "@/components/ListItems";
export default {
  name: 'ListView',
  components: {
    ListItem
  },
  props:['items']
}
</script>

<style scoped>
.item{
  background: #e6e6e6;
  padding: 5px;
  margin-top: 5px;
}
</style>
