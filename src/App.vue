<template>
  <div id="app">
    <el-container>
      <el-header>
        <HeaderBar @add-note="openDialog"/>
      </el-header>
      <el-main>
        <router-view
          :notes="notes"
          @save-note="saveNote"
          @remove-note="removeNote"/>
      </el-main>

      <el-dialog
        title="Add note"
        :visible.sync="dialogVisible"
        width="50%">

        <el-form ref="form" :model="form" label-width="120px">
          <el-form-item label="Title">
            <el-input v-model="form.title" placeholder="Put some title"></el-input>
          </el-form-item>
          <el-form-item label="Description">
            <el-input type="textarea" v-model="form.desc" placeholder="Note contet"></el-input>
          </el-form-item>
        </el-form>

        <span slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false">Cancel</el-button>
          <el-button type="primary" @click="addNoteAndClose">Confirm</el-button>
        </span>
      </el-dialog>
    </el-container>
  </div>
</template>

<script>
import HeaderBar from '@/components/HeaderBar'

export default {
  name: 'VNotes',
  components: {
    HeaderBar
  },
  data: () => ({
    dialogVisible: false,
    form: {
      title: '',
      desc: '',
    },
    notes: []
  }),
  mounted () {
    this.getNotesFromLocalStorage()
  },
  methods: {
    getNotesFromLocalStorage () {
      this.notes = window.localStorage.getItem('notes')
        ? JSON.parse(window.localStorage.getItem('notes'))
        : []
    },
    openDialog () {
      this.dialogVisible = !this.dialogVisible
    },
    addNoteAndClose () {
      this.getNotesFromLocalStorage()
      this.notes.push({ ...this.form, createdAt: new Date().getTime() })
      window.localStorage.setItem('notes', JSON.stringify(this.notes))
      this.form = {}
      this.dialogVisible = false
    },
    removeNote (index) {
      this.notes.splice(index, 1)
      window.localStorage.setItem('notes', JSON.stringify(this.notes))
    },
    saveNote ({ note, index }) { 
      this.notes[index] = note
      window.localStorage.setItem('notes', JSON.stringify(this.notes))
    }
  }
}
</script>
