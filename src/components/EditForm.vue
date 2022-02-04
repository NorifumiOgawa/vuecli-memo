<template>
  <div>
    <p><textarea v-model="memoBody" placeholder="add new memo"></textarea></p>
    <button @click='saveMemo'>save</button>
    <button @click='delMemo'>delete</button>
  </div>
</template>

<script>
export default {
  props: ['memo'],
  data(){
    return {
      editMemo: '',
      memoBody: ''
    }
  },
  mounted() {
    this.refreshMemo()
  },
  methods: {
    refreshMemo: function() {
      this.editMemo = this.memo
      this.memoBody = this.memo.body
    },
    saveMemo: function(){
      this.editMemo.body = this.memoBody
      this.$emit('saveMemo', this.editMemo)
      this.memoBody = ''
    },
    delMemo: function(){
      this.$emit('delMemo', this.editMemo)
    }
  },
  watch: {
    memo: function() {
      this.refreshMemo()
    }
  }
}
</script>

<style scoped>
div{
    border: 1px solid red
}
h2{
    color: red
}
p{
    color: red
}
</style>