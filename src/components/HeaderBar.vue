<template>
  <el-row :gutter="10" style="display: flex; align-items: center">
    <el-col :span="20">
      <h1 style="color: #444">VNotes :)</h1>
    </el-col>
    <el-col :span="4">
      <el-button
        @click="$emit('add-note')"
        type="primary"
        icon="el-icon-plus">Add note</el-button>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'ListNotes'
}
</script>
