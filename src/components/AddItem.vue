<template>
  <div class="addItem">
    <input type="text" v-model="item.name" @keyup.enter="addItem()"/>
    <button :class="[ item.name ? 'active' : 'inactive', 'default']"
            @click="addItem()">Add
    </button>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'AddView',
  components: {},
  data: function () {
    return {
      url: process.env.API_URL,
      item: {
        name: ''
      }
    }
  },
  methods: {
    addItem() {
      if (this.item.name) {
        axios.post(`${process.env.VUE_APP_API_URL}item/store`, {
          item: this.item
        }).then((d) => {
          console.log(d)
          if (d.status === 201) {
            this.item.name = ''
            this.$emit('realoadList')
          }
        }).catch((d)=> {
          console.log(d)
        })
      } else {
        return
      }
    }
  }
}
</script>

<style scoped>
.addItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

.active {
  color: black;
}

.inactive {
  color: #999999;
}

input {
  background: #f7f7f7;
  border: 0;
  outline: none;
  padding: 5px;
  margin: 10px;
  width: 100%;
}

.default {
  border: none;
  padding: 5px;
  border-radius: 1px;
}
</style>
