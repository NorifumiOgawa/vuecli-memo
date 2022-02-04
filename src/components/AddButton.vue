<template>
  <div>
    <p><label @click="openNewMemo">+</label></p>
  </div>
</template>

<script>
export default {
  methods: {
    openNewMemo() {
      this.$emit("openNewMemo");
    }
  }
}
</script>

<style scoped>
div{
    border: 1px solid green
}
h1{
    color: green
}
p{
    color:green
}
</style>