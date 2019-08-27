<template>
  <div class="form-container">
    <h3>{{formTitle}}</h3>
    <div>
      <input type="text" v-model="userData.firstName" />
      <input type="text" v-model="userData.lastName" />
      <button @click="handleBtnClicked()" :disabled="invalidInput">Save</button>
      <button @click="handleCancelClicked()">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormComponent",
  props: {
    initialFormData: Object,
  },
  data() {
    return {
      userData: {}
    };
  },
  computed: {
    formTitle: function() {
      return this.initialFormData.id !== undefined
        ? "Editing User: " + this.initialFormData.id
        : "Create User";
    },
    invalidInput: function() {
      if (!this.userData.firstName || !this.userData.lastName) {
        return true;
      } else {
        return false;
      }
    }
  },
  watch: {
    initialFormData: function(_initialData) {
      if (_initialData.name) {
        this.userData = { ..._initialData.name };
      }
    }
  },
  methods: {
    handleBtnClicked: function() {
      var returnVal = {};
      if (this.initialFormData.id !== undefined) {
        returnVal = {
          id: this.initialFormData.id,
          name: this.userData
        };
      } else {
        returnVal = this.userData;
      }
      this.$emit("form-clicked", returnVal);
      // clear the ui
      this.userData = {};
    },
    handleCancelClicked: function() {
      this.$emit("form-canceled", {});

      this.userData = {};
    }
  },
  created() {}
};
</script>

