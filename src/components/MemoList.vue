<template>
  <div>
    <ul>
      <li v-for="memo in memos" :key="memo.id"><a @click="memoSelected(memo)" href="#">{{ memoTitle(memo) }}</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    memos: Array
  },
  methods: {
    memoSelected: function(memo) {
      this.$emit('memoSelected', memo)
    },
    memoTitle: function(memo) {
      const lines = memo.body.split(/\n/)
      return lines[0]
    }
  }
}
</script>

<style scoped>
div {
  padding: 5px 0;
}
li {
  list-style-type: none;
}
</style>