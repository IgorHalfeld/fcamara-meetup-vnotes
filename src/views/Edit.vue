<template>
  <el-row :gutter="10" style="display: flex; justify-content: center;">
    <el-col :span="12">
      <el-form ref="form" :model="form" label-width="120px">
        <el-form-item label="Title">
          <el-input v-model="form.title" placeholder="Put some title"></el-input>
        </el-form-item>
        <el-form-item label="Description">
          <el-input type="textarea" v-model="form.desc" placeholder="Note contet"></el-input>
        </el-form-item>
        <el-button type="primary" @click="saveAndReturn">Save</el-button>
      </el-form>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'Edit',
  data: () => ({
    form: {
      title: '',
      desc: ''
    }
  }),
  mounted () {
    this.getNotesFromLocalStorage()
  },
  methods: {
    getNotesFromLocalStorage () {
      const { id } = this.$route.params
      const notes = window.localStorage.getItem('notes')
        ? JSON.parse(window.localStorage.getItem('notes'))
        : []
      
      this.form.title = notes[id].title
      this.form.desc = notes[id].desc
    },
    saveAndReturn () {
      this.$emit('save-note', { note: this.form, index: this.$route.params.id })
      this.$router.push({ name: 'List' })
    }
  }
}
</script>
