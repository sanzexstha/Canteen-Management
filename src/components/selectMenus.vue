<template>
<div id="menuList" >
  <!-- <h1> AAYULOGIC CANTEEN MANAGEMENT </h1> -->
<hr> <h3> Food Listings </h3> <hr>
  <router-link to="/SelectItems" tag="button"> Verify </router-link>
    <hr style="visibility: hidden; ">
  <!-- <pre>You can select only one of the items.</pre> -->
  <div class="column">
    <table id="FoodMenu" >
      <thead>
      <tr>
        <th>Id</th>
        <th>Items Available</th>
      </tr>
      </thead>
      <tr v-for="item in items" :key="item.id" @click="selectElement(item)" style="cursor: pointer">
          <td> {{ item.id }} </td>
          <td> {{ item.name }} </td>
      </tr>
    </table>
  </div>
  <div class="column">
    <table id="FoodMenu">
    <thead>
      <tr>
        <th>Id</th>
        <th>Items for Tomorrow</th>
        <th></th>
      </tr>
    </thead>
      <tr  v-for="thing in selectedItems" :key="thing.id" style="cursor: pointer">
        <td> {{ thing.id }} </td>
        <td> {{ thing.name }} </td>
        <td  @click="removeItem(thing.id)" style="cursor: pointer"> Remove </td>
      </tr>
    </table>
  </div>
</div>
</template>

<script>

export default {
  name: 'menuList',
  data () {
    return {
      selectItem: []
    }
  },
  methods: {
    selectElement: function (item) {
      this.$store.dispatch('selectItem', item)
      this.selectItem = item
    },
    removeItem: function (id) {
      this.$store.dispatch('deleteItem', id)
    }
  },
  computed: {
    items: function () {
      return this.$store.getters.items
    },
    selectedItems: function () {
      return this.$store.getters.selectedItems
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

#FoodMenu {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
  height: 100px;
  overflow-y: scroll;
}

#FoodMenu th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #404040;
  color: white;
}
#FoodMenu td, th {
  border: 1px solid #404040;
  padding: 8px;
}

#FoodMenu tr:nth-child(even){background-color: #f2f2f2;}

#FoodMenu tr:hover {background-color: #ddd;}

.column {
  float: left;
  width: 50%;
  padding: 10px;
}

* {
  box-sizing: border-box;

}
button {
  background-color: #404040;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

button:hover { background-color: #7c7575}

.header {
  background-color: #404040;
}

.highlight {
     background-color: red;
}
</style>
