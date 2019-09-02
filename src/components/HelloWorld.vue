<template>
	<div>
		<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
      <el-form-item label="图片" prop="image">
        <my-upload v-model="ruleForm.image"></my-upload>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
    </el-form>
	</div>
</template>

<script>
import MyUpload from './MyUpload'
export default {
    name: 'hello-world',
    components: {
      MyUpload
    },

    data() {
      return {
        ruleForm: {
          image: '',
        },
        rules: {
          image: [{
            required: true,
            message: '请上传图片',
            trigger: 'change'
          }],
        }
      }
    },

    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
}
</script>
