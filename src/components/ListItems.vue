<template>
  <div id="item">
    <div class="left">
      <input type="checkbox" @change="updateCheck()" v-model="item.completed" />
    </div>
    <span :class="[item.completed ? 'completed' : '','itemText' ]">{{item.name}}</span>
    <div class="right">
      <button @click="removeItem()" class="remove">Remove</button>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: 'ListItem',
  props:['item'],
  components: {
  },
  methods:{
    updateCheck() {
      axios.put(`${process.env.VUE_APP_API_URL}item/${this.item.id}`,{
        item: this.item
      }).then((d) => {
        console.log(d)
        if (d.status === 200) {
          this.$emit('itemChanged');
        }
      }).catch((d)=> {
        console.log(d)
      })
    },
    removeItem() {
      axios.delete(`${process.env.VUE_APP_API_URL}item/${this.item.id}`).then((d) => {
        if (d.status === 200) {
          this.$emit('itemChanged')
        }
      }).catch((d)=> {
        console.log(d)
      })
    }
  }
}
</script>

<style scoped>
#item{
  display: flex;
  align-items: center;
  vertical-align: top;
  padding-left: 25px;
  position: relative;
}
.completed{
text-decoration: line-through;
  color: #999999;
}
.itemText{
  margin-left: 20px;
}
input{
  position: absolute;
  top: 5px;
  left: 0;
}
.right{
text-align: right;
}
.remove{
  position: absolute;
  top: 3px;
  right: 0;
}
</style>
