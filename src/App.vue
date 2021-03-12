<template>
  <div class="todolistcontainer">
    <div class="heading">
        <h2 id="tital" >Todo List</h2>
      <add-item  v-on:realoadList="getList()"/>
    </div>
    <ListView :items="items" v-on:realoadList="getList()"/>
  </div>
</template>

<script>
import AddItem from "@/components/AddItem";
import ListView from "@/components/ListView";
import axios from "axios";


export default {
  name: 'App',
  components: {
    AddItem,
    ListView,
  },
  data:function () {
    return{
      items:[]
    }
  },
  methods:{
    getList() {
      axios.get(`${process.env.VUE_APP_API_URL}items`).then((d) => {
        this.items = d.data
        console.log(d)
      }).catch((d) => {
        console.log(d)
      })
    },
  },
  created() {
    this.getList()
  },
}
</script>

<style>
.todolistcontainer{
  width: 350px;
  margin: auto;
}
.heading{
  background: #e6e6e6;
  padding: 10px;
}
#tital{
  text-align: center;
}
</style>
