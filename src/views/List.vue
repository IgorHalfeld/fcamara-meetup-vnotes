<template>
  <div style="display: flex; justify-content: space-around">
    <el-card
      v-for="(note, index) in notes"
      :key="index"
      class="box-card"
      style="flex-basis: 320px">
      <div slot="header" class="clearfix">
        <span>{{ note.title }}</span>
        <el-button
          @click="$emit('remove-note', index)"
          style="float: right; padding: 5px"
          type="danger"
          icon="el-icon-delete">Remove</el-button>
        <el-button
          @click="goToEditRoute(index)"
          style="float: right; padding: 5px"
          type="default"
          icon="el-icon-edit">Edit</el-button>
      </div>
      <div class="text item">
        {{ note.desc }}
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    notes: { type: Array, default: () => ([]) }
  },
  methods: {
    goToEditRoute (index) {
      this.$router.push({ name: 'Edit', params: { id: index } })
    }
  }
}
</script>
