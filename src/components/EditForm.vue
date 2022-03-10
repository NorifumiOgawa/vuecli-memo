<template>
  <div>
    <p><textarea class="form-control memoBody" v-model="editMemo.body" placeholder="add new memo"></textarea></p>
    <button class="btn btn-primary" @click='emitMemo'>save</button>
    <button class="btn btn-secondary" @click='deleteMemo'>delete</button>
  </div>
</template>

<script>
export default {
  props: {
    memo: Object
  },
  data () {
    return {
      editMemo: ''
    }
  },
  mounted () {
    this.refreshMemo()
  },
  methods: {
    refreshMemo () {
      this.editMemo = { ...this.memo }
    },
    emitMemo () {
      if (!this.editMemo.body) { return false }
      this.$emit('saveMemo', this.editMemo)
    },
    deleteMemo () {
      this.$emit('deleteMemo', this.editMemo)
    }
  },
  watch: {
    memo () {
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
