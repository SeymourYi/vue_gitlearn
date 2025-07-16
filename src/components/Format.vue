<template>
  <div>
    <el-form :model="mainForm" label-width="120px" style="max-width: 600px; margin: 40px auto;">
      <el-form-item label="姓名">
        <el-input v-model="mainForm.name" />
      </el-form-item>
      <el-form-item label="邮箱">
        <el-input v-model="mainForm.email" />
      </el-form-item>
      <el-form-item label="年龄">
        <el-input v-model="mainForm.age" type="number" />
      </el-form-item>
      <el-form-item label="地址">
        <el-input v-model="mainForm.address" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="dialogVisible = true">弹出表单</el-button>
      </el-form-item>
    </el-form>
    <el-dialog v-model="dialogVisible" title="弹出表单" width="400px">
      <el-form :model="dialogForm" label-width="100px" :rules="dialogRules" ref="dialogFormRef">
        <el-form-item label="备注">
          <el-input v-model="dialogForm.remark" />
        </el-form-item>
        <el-form-item label="性别" prop="sex">
          <el-select v-model="dialogForm.sex" placeholder="请选择性别" clearable>
            <el-option label="男" value ="男" />
            <el-option label="女" value ="女" />
          </el-select>
        </el-form-item>
        <el-form-item label="手机号" prop="sssss">
          <el-input v-model="dialogForm.phone" />
        </el-form-item>
      </el-form>
      <template #footer>
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="submitDialogForm">提交</el-button>
      </template>
    </el-dialog>
  </div>
</template>

<script setup lang="ts">
import { setTextRange } from 'typescript'
import { ref } from 'vue'

const mainForm = ref({
  name: '',
  email: '',
  age: '',
  address: ''
})

const dialogVisible = ref(false)
const dialogForm = ref({
  remark: '',
  phone: '',
  sex: null
})
const dialogFormRef = ref()
const dialogRules = {
  sssss: [
    { required: true, message: '手机号为必填项', trigger: 'blur' }
  ],
  sex: [
    { required: true, message: '性别为必填项', trigger: 'change' }
  ]
}
function submitDialogForm() {
  dialogFormRef.value?.validate((valid: boolean) => {
    if (valid) {
      dialogVisible.value = false
      // 这里可以添加弹窗表单的提交逻辑
      console.log('弹窗表单数据:', dialogForm.value)
    }
  })
}
</script>

<style scoped>
.el-form {
  background: #fafafa;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}
</style>