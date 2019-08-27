<template>
  <div id="app">
    <img
      alt="random image of cat to serve as a placeholder for something meaningful"
      src="https://placekitten.com/300/100"
    />
    <list-component
      :incomingListData="userArray"
      @list-clicked="handleListClicked"
      @delete-item="handleDeleteListItem"
      @edit-item="handleEditListItem"
    ></list-component>
    <template v-if="inEditMode">
      <form-component
        :initialFormData="editingUser"
        @form-clicked="handleFormEdit"
        @form-cancelled="handleFormCancelled"
      ></form-component>
    </template>
    <template v-else>
      <form-component
        :initialFormData="{}"
        @form-clicked="handleFormClicked"
        @form-cancelled="handleFormCancelled"
      ></form-component>
    </template>
  </div>
</template>

<script>
import ListComponent from "./components/ListComponent.vue";
import FormComponent from "./components/FormComponent.vue";

export default {
  name: "app",
  data() {
    return {
      editingUser: {},
      userArray: [
        { id: 0, name: { firstName: "Ada", lastName: "Lovelace" } },
        { id: 1, name: { firstName: "Alan", lastName: "Turing" } },
        { id: 2, name: { firstName: "Grace", lastName: "Hopper" } }
      ]
    };
  },
  computed: {
    inEditMode: function() {
      return this.editingUser.id != undefined ? true : false;
    }
  },
  components: {
    ListComponent,
    FormComponent
  },
  methods: {
    handleListClicked: function(_data) {
      alert(_data.name.firstName + " " + _data.name.lastName);
    },

    handleEditListItem: function(_item) {
      alert(_item.name.firstName + " " + _item.name.lastName);
      this.editingUser = { ..._item };
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
    },

    handleFormEdit: function(_item) {
      console.log("handleFormEdit", _item);
      let edited = this.userArray.map(item => {
        if (item.id == _item.id) {
          return { ..._item };
        } else {
          return item;
        }
      });
      this.userArray = edited;
      this.editingUser = {};
    },

    handleFormCancelled: function(_data) {
      console.log(_data);
      this.editingUser = {};
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
