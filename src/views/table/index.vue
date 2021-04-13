<!--
 * @Author: yuan.zhou
 * @Date: 2021-03-06 13:50:05
 * @Descripton: 表格+表单聚合
 * @LastEditTime: 2021-04-13 08:54:56
-->
<template>
  <div class="app-container">
    <el-button class="filter-item" style="margin-left: 10px;" type="primary" icon="el-icon-edit" @click="handleCreate">
      新增
    </el-button>

    <el-dialog :title="textMap[dialogStatus]" :visible.sync="dialogOneFormVisible">
      <el-form ref="dataForm" :rules="oneFormRules" :model="oneForm" label-position="left" label-width="70px" style="width: 400px; margin-left:50px;">
        <el-form-item label="Type" prop="type">
          <!-- <el-select v-model="oneForm.type" class="filter-item" placeholder="Please select">
            <el-option v-for="item in calendarTypeOptions" :key="item.key" :label="item.display_name" :value="item.key" />
          </el-select> -->
        </el-form-item>
        <el-form-item label="Date" prop="timestamp">
          <el-date-picker v-model="oneForm.timestamp" type="datetime" placeholder="Please pick a date" />
        </el-form-item>
        <el-form-item label="Title" prop="title">
          <el-input v-model="oneForm.title" />
        </el-form-item>
        <el-form-item label="Status">
          <!-- <el-select v-model="oneForm.status" class="filter-item" placeholder="Please select">
            <el-option v-for="item in statusOptions" :key="item" :label="item" :value="item" />
          </el-select> -->
        </el-form-item>
        <el-form-item label="Imp">
          <el-rate v-model="oneForm.importance" :colors="['#99A9BF', '#F7BA2A', '#FF9900']" :max="3" style="margin-top:8px;" />
        </el-form-item>
        <el-form-item label="Remark">
          <el-input v-model="oneForm.remark" :autosize="{ minRows: 2, maxRows: 4}" type="textarea" placeholder="Please input" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogOneFormVisible = false">
          Cancel
        </el-button>
        <el-button type="primary" @click="dialogStatus==='create'?createData():updateData()">
          Confirm
        </el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import { getList } from '@/api/table'

export default {
  data() {
    return {
      list: null,
      textMap: {add: '新增', edit: '编辑'},
      dialogStatus: 'add',
      dialogOneFormVisible: false,
      oneForm: {},
      oneFormRules: {

      }
    }
  },
  methods: {
    handleCreate() {
      this.dialogOneFormVisible = true;
      
    },
    fetchData() {
      this.listLoading = true
      getList().then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    }
  },
  created() {
    this.fetchData()
  },
}
</script>
