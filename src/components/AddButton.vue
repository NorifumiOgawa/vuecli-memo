<template>
  <div>
    <p><a class="openNewMemo" @click="openNewMemo" href="#">＋</a></p>
  </div>
</template>

<script>
export default {
  methods: {
    openNewMemo () {
      this.$emit('openNewMemo')
    }
  }
}
</script>

<style scoped>
.openNewMemo {
  margin-left: 30px;
  text-decoration:none;
}
</style>
