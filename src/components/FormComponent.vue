<template>
  <div class="form-container">
    <h3>My Form Component</h3>
    <div>
      <input type="text" v-model="userData.firstName" />
      <input type="text" v-model="userData.lastName" />
      <button @click="handleBtnClicked()">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormComponent",
  props: {
    initialFormData: Object,
  },
  data: function() {
    return {
      userData: this.initialFormData.name || {}
    };
  },
  methods: {
    handleBtnClicked: function() {
      this.$emit("form-clicked", this.userData);
      // clear the ui
      this.userData = {};
    }
  }
};
</script>

