<template>
  <Container>
    <PageHeader
      slot="header"
      title="导出表格">
    </PageHeader>
    <div class="dd-mb">
      <el-button type="primary" @click="exportCsv">
        <Icon name="download"></Icon>
        导出 CSV
      </el-button>
      <el-button type="primary" @click="exportExcel">
        <Icon name="download"></Icon>
        导出 Excel
      </el-button>
    </div>
    <el-table v-bind="table" style="width: 100%" class="dd-mb">
      <el-table-column
        v-for="(item, index) in table.columns"
        :key="index"
        :prop="item.prop"
        :label="item.label">
      </el-table-column>
    </el-table>
    <Markdown url="/static/md/插件 - 导出.md"></Markdown>
  </Container>
</template>

<script>
// 假数据
import table from './data'
export default {
  data () {
    return {
      table: {
        columns: table.columns,
        data: table.data,
        size: 'mini',
        stripe: true,
        border: true
      }
    }
  },
  methods: {
    exportCsv (params = {}) {
      this.$export.csv({
        columns: this.table.columns,
        data: this.table.data
      })
        .then(() => {
          this.$message('导出CSV成功')
        })
    },
    exportExcel () {
      this.$export.excel({
        columns: this.table.columns,
        data: this.table.data
      })
        .then(() => {
          this.$message('导出表格成功')
        })
    }
  }
}
</script>
