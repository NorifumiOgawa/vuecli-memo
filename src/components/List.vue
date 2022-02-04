<template>
  <div>
    <h1>VueCLI Memo</h1>
    <ul>
      <li v-for="memo in memos" :key="memo.id"><label @click="memoSelected(memo)">{{ memoTitle(memo) }}</label></li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['memos'],
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
div{
    border: 1px solid blue
}
h1{
    color: blue
}
p{
    color:blue
}
</style>