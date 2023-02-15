<template>
  <div class="app-container">
    <el-form ref="employeeForm" :rules="rules" :model="employeeForm" label-width="150px">
      <el-form-item label="Код сотрудника" prop="code">
        <el-input v-model="employeeForm.employeeCode" placeholder="Код сотрудника" />
      </el-form-item>
      <el-form-item label="Фамилия" prop="lastName">
        <el-input v-model="employeeForm.lastName" placeholder="Фамилия" />
      </el-form-item>
      <el-form-item label="Имя" prop="firstName">
        <el-input v-model="employeeForm.firstName" placeholder="Имя" />
      </el-form-item>
      <el-form-item label="Отчество" prop="surName">
        <el-input v-model="employeeForm.surName" placeholder="Отчество" />
      </el-form-item>
      <el-form-item label="Телефон" prop="phone">
        <el-input v-model="employeeForm.phone" placeholder="Номер телефона сотрудника" />
      </el-form-item>
      <el-form-item label="Адрес" prop="address">
        <el-input v-model="employeeForm.address" placeholder="Адрес сотрудника" />
      </el-form-item>
      <el-form-item label="Должность" prop="position">
        <el-input v-model="employeeForm.position" placeholder="Должность" />
      </el-form-item>
      <el-form-item label="Электронная почта" prop="email">
        <el-input v-model="employeeForm.email" placeholder="Электронная почта" />
      </el-form-item>
      <el-form-item label="Загрузить резюме" prop="resume">
        <!-- <el-input v-model="employeeForm.resume" placeholder="Загрузить резюме" /> -->
        <el-upload
          class="upload-demo"
          :auto-upload="false"
          :on-remove="handleRemove"
          :on-change="uploadChange"
          action="#"
          :file-list="fileList"
          list-type="picture"
        >
          <el-button size="small" type="primary">Click to upload</el-button>
          <div slot="tip" class="el-upload__tip">jpg/png files with a size less than 500kb</div>
        </el-upload>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('employeeForm')">Отправить</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import { createEmployee } from '@/api/employee'
export default {
  name: 'ComponentMixinDemo',
  data() {
    return {
      file: {},
      fileList: [],
      employeeForm: {
        employeeCode: '',
        firstName: '',
        lastName: ''
      },
      rules: {
        employeeCode: [
          { required: true, message: 'Field is required', trigger: 'blur' }
        ],
        lastName: [
          { required: true, message: 'Field is required', trigger: 'blur' }
        ],
        firstName: [
          { required: true, message: 'Field is required', trigger: 'blur' }
        ],
        surName: [
          { required: true, message: 'Please select Activity zone', trigger: 'change' }
        ]
      }
    }
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePreview(file) {
      console.log(file)
    },
    uploadChange(file) {
      console.log(file)
      this.file = file
    },
    submitForm(formName) {
      console.log('22', formName)
      this.$refs[formName].validate((valid) => {
        if (valid) {
          const fb = new FormData()

          fb.append('file', this.file)

          createEmployee({ dto: this.employeeForm, file: fb })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>
