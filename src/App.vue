<template>
  <div id="app">
    <img
      alt="random image of cat to serve as a placeholder for something meaningful"
      src="https://placekitten.com/300/100"
    />
    <form-component :initialFormData="{}" @form-clicked="handleFormClicked"></form-component>
    <list-component
      :incomingListData="userArray"
      @list-clicked="handleListClicked"
      @delete-item="handleDeleteListItem"
    ></list-component>
  </div>
</template>

<script>
import ListComponent from "./components/ListComponent.vue";
import FormComponent from "./components/FormComponent.vue";

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
    ListComponent,
    FormComponent
  },
  methods: {
    handleWasClicked: function(_data) {
      alert(_data);
    },

    handleListClicked: function(_data) {
      alert(_data.name.firstName + " " + _data.name.lastName);
    },
    handleDeleteListItem: function(_item) {
      console.log("deleteListElement", _item);
      let result = this.userArray.filter(element => {
        return element.id != _item.id;
      });
      this.userArray = result;
    },

    handleFormClicked: function(_data) {
      console.log(_data);
      this.userArray.push({
        name: _data,
        id: new Date().getTime()
      });
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
