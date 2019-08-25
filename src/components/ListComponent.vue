<template>
  <div>
    <h3>Show List Of Users</h3>
    <ol>
      <li v-for="e in this.incomingListData" :key="e.id">
        <span @click="$emit('list-clicked', e)">{{ e.name.firstName }} {{ e.name.lastName }}</span>
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
  methods: {}
};
</script>

