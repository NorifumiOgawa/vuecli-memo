<template>
  <div>
    <p><textarea class="form-control memoBody" v-model="memoBody" placeholder="add new memo"></textarea></p>
    <button class="btn btn-primary" @click='saveMemo'>save</button>
    <button class="btn btn-secondary" @click='delMemo'>delete</button>
  </div>
</template>

<script>
export default {
  props: {
    memo: Object
  },
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
button {
  margin-right: 5px
}

.memoBody {
  height: 300px;
}
</style>