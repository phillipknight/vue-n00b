<template>
  <div>
    <h3>Show List Of Users</h3>
    <ol>
      <li v-for="listItem in this.incomingListData" :key="listItem.id">
        <span
          @click="handleItemClicked(listItem)"
        >{{ listItem.name.firstName }} {{ listItem.name.lastName }}</span>
        <button @click="handleDeleteItemClicked(listItem)">DELETE</button>
        <button @click="handleEditItemClicked(listItem)">EDIT</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "ListComponent",
  props: {
    incomingListData: Array
  },
  methods: {
    handleItemClicked: function(_listItem) {
      this.$emit('list-clicked', _listItem);
    },
    handleDeleteItemClicked: function(_listItem) {
      this.$emit('delete-item', _listItem);
    },
    handleEditItemClicked: function(_listItem) {
      this.$emit('edit-item', _listItem);
    }
  },
};
</script>

