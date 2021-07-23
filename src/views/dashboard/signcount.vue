<template>
  <el-table :data="tableData" border style="width: 100%">
    <el-table-column fixed prop="class" label="班级" width="150">
    </el-table-column>
    <el-table-column prop="date" label="入学年份" width="120">
    </el-table-column>
    <el-table-column prop="classname" label="课程名称" width="120">
    </el-table-column>
    <el-table-column prop="teachername" label="任课老师" width="120">
    </el-table-column>
    <el-table-column prop="classdate" label="上课时间" width="100">
    </el-table-column>
    <el-table-column prop="nums" label="班级人数" width="100">
    </el-table-column>
    <el-table-column prop="chuqin" label="出勤" width="100">
    </el-table-column>
    <el-table-column prop="queqin" label="缺勤" width="100">
    </el-table-column>
    <el-table-column prop="shijia" label="事假" width="100">
    </el-table-column>
    <el-table-column prop="bingjia" label="病假" width="100">
    </el-table-column>
    <el-table-column prop="chidao" label="迟到" width="100">
    </el-table-column>
    <el-table-column prop="zaotui" label="早退" width="100">
    </el-table-column>
    <el-table-column prop="uploaddata" label="更新时间" width="120">
    </el-table-column>
    <el-table-column label="操作" width="100">
      <template slot-scope="scope">
        <el-button size="small" type="text" @click="handleClick(scope.row)">查看</el-button>
        <el-button type="text" size="small">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>
  <!-- 页脚部分 -->
</template>

<script>
export default {
  methods: {
    handleClick(row) {
      console.log(row)
    },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`)
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`)
      }
  },

  data() {
    return {
      tableData: [{
        class: '01',
        date: '2016-05-02',
        classname: 'shixin',
        teachername: 'yh',
        classdate: '1212',
        nums: '王小虎',
        chuqin: '上海',
        queqin: '普陀区',
        shijia: '上海市普陀区金沙江路 1518 弄',
        bingjia: 200333,
        chidao: '1',
        zaotui: '2',
        uploaddata: '111'
      }]
    }
  }
}
</script>
