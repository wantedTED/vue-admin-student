<template>
  <!-- <div class="dashboard-container">
    <div class="dashboard-text">name: {{ name }}</div>
  </div> -->
  <div class="searchform-container">
    <el-form ref="searchform" :model="parms" :rules="rules" label-width="80px" :inline="true" size="small">
      <el-form-item>
        <el-button type="primary" @click="onSubmit">导入</el-button>
        <el-button type="primary" @click="onSubmit">新增</el-button>
        <el-button type="primary" @click="onSubmit">导出</el-button>
        <el-button type="danger" style="margin-right:110px" @click="onSubmit">删除</el-button>
      </el-form-item>

      <!-- 选择按钮 -->
      <el-select v-model="grades" placeholder="入学年份" size="small" style="margin-right:10px">
        <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
        </el-option>
      </el-select>
      <el-select v-model="classes" placeholder="班级" size="small">
        <el-option v-for="item in options1" :key="item.value" :label="item.label" :value="item.value">
        </el-option>
      </el-select>
      <el-form-item label="学号">
        <el-input v-model="parms.stdent_id"></el-input>
      </el-form-item>
      <el-form-item label="姓名">
        <el-input v-model="parms.name"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">搜索</el-button>
      </el-form-item>
    </el-form>

    <!-- 表格部分 -->
    <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55">
      </el-table-column>
      <el-table-column label="入学年份" width="250">
        <template slot-scope="scope">{{ scope.row.date }}</template>
      </el-table-column>
      <el-table-column prop="class" label="班级" width="250">
      </el-table-column>
      <el-table-column prop="student_id" label="学号" width="250">
      </el-table-column>
      <el-table-column prop="name" label="姓名" width="250">
      </el-table-column>
    </el-table>
    <!-- 页脚部分 -->
    <span class="demonstration"></span>
    <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage4" :page-sizes="[100, 200, 300, 400]" :page-size="100" layout="total, sizes, prev, pager, next, jumper" :total="400">
    </el-pagination>
  </div>
</template>

<script>
// import { mapGetters } from 'vuex'

export default {
  // name: 'Dashboard',
  // computed: {
  //   ...mapGetters([
  //     'name'
  //   ])
  // }
  data() {
    return {
      parms: {
        student_id: '',
        name: ''
      },
      options: [{
        value: '选项1',
        label: '2020'
      }, {
        value: '选项2',
        label: '2019'
      }, {
        value: '选项3',
        label: '2018'
      }],
      options1: [{
        value: '选项1',
        label: '一班'
      }, {
        value: '选项2',
        label: '二班'
      }, {
        value: '选项3',
        label: '三班'
      }],
      tableData: [{
        date: '2016-05-03',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-02',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-08',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-06',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }, {
        date: '2016-05-07',
        name: '王小虎',
        class: '1class',
        student_id: '001'
      }],
      multipleSelection: [],
      grades: '',
      classes: ''
    }
  },
  methods: {
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }

  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}

.searchform-container {
  margin: 10px;

}
</style>
