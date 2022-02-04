<template>
  <div>
    <List @memoSelected="memoSelected" :memos="memos"></List>
    <AddButton @openNewMemo="openNewMemo"></AddButton>
    <EditForm v-if="editing || adding" @saveMemo="saveMemo" @delMemo="delMemo" :memo="this.editingMemo"></EditForm>
  </div>
</template>

<script>
import List from './components/List.vue'
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
    List,
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
    delMemo(editMemo){
      const new_memos = this.memos.filter(v => {
        if(v.id != editMemo.id) { return true}
      })
      memoStorage.save(new_memos)
      this.memos = new_memos
      this.editing = false
      this.adding = false
    }
  }
}
</script>
