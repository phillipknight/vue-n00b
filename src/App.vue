<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <list-component :incomingListData="userArray" @list-clicked="handleListClicked"></list-component>
  </div>
</template>

<script>
import ListComponent from "./components/ListComponent.vue";

export default {
  name: "app",
  data: function() {
    return {
      userArray: [
        { id: 0, name: { firstName: "Ada", lastName: "Lovelace" } },
        { id: 1, name: { firstName: "Alan", lastName: "Turing" } },
        { id: 2, name: { firstName: "Grace", lastName: "Hopper" } }
      ],
      current: {},
      newUser: {}
    };
  },
  components: {
    ListComponent
  },
  methods: {
    handleWasClicked: function(_name, _date) {
      alert(`that component was clicked and the name is ${_name} ${_date}`);
    },
    handleListClicked: function(_data) {
      alert(_data.name.firstName);
    },
    makeCurrent: function(_item) {
      this.current = _item;
    },
    editItem: function(_item) {
      this.newUser = JSON.parse(JSON.stringify(_item));
    },
    cancelAction: function() {
      this.newUser = { name: {} };
    },
    updateItem: function(_item) {
      let edited = this.userArray.map(item => {
        if (item.id == _item.id) {
          return { ..._item };
        } else {
          return item;
        }
      });

      this.userArray = edited;
      this.newUser = { name: {} };
    },
    addItem: function() {
      this.userArray.push({
        name: this.newUser.name,
        id: new Date().getTime()
      });
      // clear UI
      this.newUser = { name: {} };
    },
    deleteItem: function(_item) {
      let result = this.userArray.filter(element => {
        return element.id != _item.id;
      });
      this.userArray = result;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
