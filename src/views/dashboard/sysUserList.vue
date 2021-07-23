<template>
  <el-main height="100%">
    <!-- Main content -->
    <el-form :model="parms" ref="form" :rules="rules" label-width="80px" :inline="true" size="small">
      <el-form-item label="姓名">
        <el-input v-model="parms.userName"></el-input>
      </el-form-item>
      <el-form-item label="电话">
        <el-input v-model="parms.phone"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button icon="el-icon-search">查询</el-button>
        <el-button type="primary" icon="el-icon-plus" @click="addUser">新增</el-button>
      </el-form-item>
    </el-form>
    <!-- 表格 -->
    <el-table :data="tableList" :height="tableHeight" size="small" empty-text="暂无数据" border stripe>
      <el-table-column prop="userName" label="姓名"></el-table-column>
      <el-table-column prop="phone" label="电话"></el-table-column>
      <el-table-column prop="idCard" label="身份证"></el-table-column>
      <el-table-column prop="sex" label="性别"></el-table-column>
      <el-table-column prop="status" label="是否离职"></el-table-column>
      <el-table-column prop="isUsed" label="账号状态"></el-table-column>
    </el-table>
    <!-- 分页 -->
    <el-pagination @size-change="sizeChange" @current-change="currentChange" :current-page.sync="parms.currentPage" :page-sizes="[10, 20, 30, 40, 50]" :page-size="parms.pageSize" layout="total, sizes, prev, pager, next, jumper" :total="parms.total" background>
    </el-pagination>
    <sys-dialog :title="dialog.title" :visible="dialog.visible" :width="dialog.width" :height="dialog.height" @onClose="onClose" @onConfirm="onConfirm">
      <div slot="content">
        <!-- 新增表单 -->
        <el-form :model="addModel" ref="addForm" :rules="rules" label-width="80px" :inline="true" size="small">
          <el-form-item prop="userName" label="姓名:">
            <el-input v-model="addModel.userName"></el-input>
          </el-form-item>
          <el-form-item label="性别:" prop="sex" style="width:264px">
            <el-radio-group v-model="addModel.sex">
              <el-radio :label="1">男</el-radio>
              <el-radio :label="0">女</el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="电话:" prop="phone">
            <el-input v-model="addModel.phone"></el-input>
          </el-form-item>
          <el-form-item label="身份证:" prop="idCard">
            <el-input v-model="addModel.idCard"></el-input>
          </el-form-item>
          <el-form-item label="登录名:" prop="loginName">
            <el-input v-model="addModel.loginName"></el-input>
          </el-form-item>
          <el-form-item label="密码:" prop="password">
            <el-input v-model="addModel.password"></el-input>
          </el-form-item>
          <el-form-item label="是否离职:" style="width:264px">
            <el-radio-group v-model="addModel.status">
              <el-radio :label="1">是</el-radio>
              <el-radio :label="0">否</el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="是否启用:" style="width:264px;height:33px">
            <el-radio-group v-model="addModel.isUsed">
              <el-radio :label="0">是</el-radio>
              <el-radio :label="1">否</el-radio>
            </el-radio-group>
          </el-form-item>
        </el-form>
      </div>
    </sys-dialog>
  </el-main>
</template>

<script>
import {
  getUserListApi
} from '@/api/user'
import sysDialog from '@/components/system/sysDialog.vue'
export default {
  // 组件使用前需要注册
  components: {
    sysDialog
  },
  data() {
    return {
      tableHeight: 0,
      // 验证表单内容使用，与onCOnfirm组合使用，完成页面必填内容
      rules: {
        userName: [{
          required: true,
          trigger: 'change',
          message: '请填写姓名'
        }],
        sex: [{
          required: true,
          trigger: 'change',
          message: '请填写性别'
        }],
        phone: [{
          required: true,
          trigger: 'change',
          message: '请填写手机号'
        }],
        idCard: [{
          required: true,
          trigger: 'change',
          message: '请填写身份证'
        }],
        loginName: [{
          required: true,
          trigger: 'change',
          message: '请填写登录名'
        }],
        password: [{
          required: true,
          trigger: 'change',
          message: '请填写密码'
        }]
      },
      addModel: {
        userName: '',
        sex: '',
        phone: '',
        idCard: '',
        loginName: '',
        password: '',
        isUsed: '',
        status: ''
      },
      dialog: {
        title: '',
        visible: false,
        height: 240,
        width: 610
      },
      parms: {
        userName: '',
        phone: '',
        currentPage: 1,
        pageSize: 10,
        total: 0
      },
      tableList: []
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.tableHeight = window.innerHeight - 300
    })
  },
  created() {
    this.getUserList()
  },
  methods: {
    // 对话框关闭
    onClose() {
      this.dialog.visible = false
    },
    addUser() {
      this.dialog.title = '新增员工'
      this.dialog.visible = true
    },
    // 确认事件
    onConfirm() {
      // this.dialog.visible = false
      this.$refs.addForm.validate(valid => {
        if (valid) {
          this.dialog.visible = false
        }
      })
    },
    async getUserList() {
      const res = await getUserListApi(this.parms)
      if (res.code === 200) {
        console.log(res)
        this.tableList = res.data.records
      }
    },
    sizeChange(val) {},
    currentChange(val) {}
  }
}
</script>

<style lang="scss" scoped>

</style>
