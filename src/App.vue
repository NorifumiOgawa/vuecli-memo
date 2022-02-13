<template>
  <div class="container">
    <div class="row">
      <div class="col-4">
        <MemoList @memoSelected="memoSelected" :memos="memos"></MemoList>
        <AddButton @openNewMemo="openNewMemo"></AddButton>
      </div>
      <div class="col-8">
        <EditForm v-if="editing || adding" @saveMemo="saveMemo" @deleteMemo="deleteMemo" :memo="editingMemo"></EditForm>
      </div>
    </div>
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'
import EditForm from './components/EditForm.vue'
import AddButton from './components/AddButton.vue'

const STORAGE_KEY = 'fjord-vuecli-memo'
const memoStorage = {
  fetch() {
    return JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  },
  save(memos) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(memos))
  }
};

export default {
  data(){
    return {
      memos: [],
      editingMemo: [],
      editing: false,
      adding: false
    }
  },
  mounted() {
    this.memos = memoStorage.fetch()
  },
  components: {
    MemoList,
    EditForm,
    AddButton
  },
  methods: {
    memoSelected(memo){
      this.editing = true
      this.editingMemo = memo
    },
    openNewMemo() {
      this.editingMemo = []
      this.adding = true
    },
    saveMemo(editMemo){
      if (!this.editingMemo.id) {
        this.memos.push({
          id: Date.now() + Math.floor(Math.random() * 100),
          body: editMemo.body
        })
      }
      memoStorage.save(this.memos)
      this.editing = false
      this.adding = false
    },
    deleteMemo(editMemo){
      const newMemos = this.memos.filter(v => v.id != editMemo.id)
      memoStorage.save(newMemos)
      this.memos = newMemos
      this.editing = false
      this.adding = false
    }
  }
}
</script>

<style>
.container {
  background-color: #ffffff;
}

body {
  background-color: #ececec !important;
}

div {
  padding: 5px 0
}
</style>
