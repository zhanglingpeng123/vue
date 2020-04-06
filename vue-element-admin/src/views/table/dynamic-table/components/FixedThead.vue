<template>
  <div class="app-container">
    <div class="filter-container">
      <el-checkbox-group v-model="checkboxVal">
        <el-checkbox label="apple">
          id
        </el-checkbox>
        <el-checkbox label="banana">
          username
        </el-checkbox>
        <el-checkbox label="orange">
          password
        </el-checkbox>
      </el-checkbox-group>
    </div>
    <el-table :key="key" :data="tableData2" border fit highlight-current-row style="width: 100%">
      <el-table-column prop="id" label="id" width="180" />
      <el-table-column v-for="fruit in formThead2" :key="fruit" :label="fruit">
        <template slot-scope="scope">
          {{ scope.row[fruit] }}
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
const defaultFormThead = ['apple', 'banana']

export default {
  data() {
    return {
      tableData2: [{ 'id': 1, 'username': 'lao', 'password': '123' }, { 'id': 2, 'username': 'li', 'password': '456' }],
      tableData: [
        {
          name: 'fruit-1',
          apple: 'apple-10',
          banana: 'banana-10',
          orange: 'orange-10'
        },
        {
          name: 'fruit-2',
          apple: 'apple-20',
          banana: 'banana-20',
          orange: 'orange-20'
        }
      ],
      key: 1, // table key
      formTheadOptions: ['apple', 'banana', 'orange'],
      checkboxVal: defaultFormThead, // checkboxVal
      formThead: defaultFormThead, // 默认表头 Default header
      formThead2: ['username', 'password']
    }
  },
  watch: {
    checkboxVal(valArr) {
      this.formThead = this.formTheadOptions.filter(i => valArr.indexOf(i) >= 0)
      this.key = this.key + 1// 为了保证table 每次都会重渲 In order to ensure the table will be re-rendered each time
    }
  },

  mounted() {
    this.test()
  },
  methods: {
    test: function() {
      this.$ajaxWrapper.get('/api/user/findAll', {
      }, response => {
        debugger
        this.tableData2 = response.data
      })
    }
  }
}
</script>

