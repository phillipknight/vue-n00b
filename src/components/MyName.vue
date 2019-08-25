<template>
<div @click="sendClick">{{ name }}</div>
</template>

<script>
export default {
  name: 'MyName',
  props: {
    name: String
  },
  methods: {
    sendClick: function() {
      this.$emit('wasClicked', this.name, new Date());
    } 
  }

}
</script>

