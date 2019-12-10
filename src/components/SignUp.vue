<template>
  <el-dialog title="注册" :visible.sync="currentDialogVisible" width="500px" center>
    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      label-position="left"
      label-width="100px"
    >
      <el-form-item label="注册邮箱" prop="email">
        <el-input v-model="ruleForm.email" placeholder="示例: admin@meethere.com"></el-input>
      </el-form-item>
      <el-form-item label="用户名" prop="userName">
        <el-input v-model="ruleForm.userName" placeholder="请输入用户名: (不超过B个字)"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" v-model="ruleForm.password" placeholder="请输入密码: (不超过B个字符)"></el-input>
      </el-form-item>
      <el-form-item label="邮件验证码" prop="code">
        <el-row type="flex" justify="space-between">
          <el-col :span="13">
            <el-input v-model="ruleForm.code"  placeholder="请输入邮件中的验证码"></el-input>
          </el-col>
          <el-col :span="6.5">
              <el-button type="primary" @click="submitForm('ruleForm')">发送验证码</el-button>
          </el-col>
        </el-row>
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button type="primary" class="submit_btn" @click="submitForm('ruleForm')">立即注册</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  name: "SignUp",
  props: ["dialogVisible"],
  data() {
    return {
      currentDialogVisible: this.dialogVisible,
      ruleForm: {
        email: "",
        userName: "",
        password: "",
        code: ""
      },
      rules: {
        email: [
          { required: true, message: "请输入注册邮箱", trigger: "blur" }
          // { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" }
        ],
        userName: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 A 到 B 个字符", trigger: "blur" }
        ],
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 A 到 B 个字符", trigger: "blur" }
        ],
        code: [
          { required: true, message: "请输入验证码", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 A 到 B 个字符", trigger: "blur" }
        ]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    }
  },
  watch: {
    dialogVisible: function(newValue) {
      this.currentDialogVisible = newValue;
    },
    currentDialogVisible: function(newValue) {
      // 只能通过观察 currentDialogVisible 来判断是否点击 X
      this.$emit("updateDialogVisible", newValue);
    }
  }
};
</script>

<style lang="less" scoped>
@import "../style/mixin";
// .form_contianer {
//   .wh(400px, 270px);
//   .ctp(400px, 270px);
//   // padding: 25px;
//   border-radius: 5px;
//   // text-align: center;
//   background-color: #fff;

// }
// .submit_btn {
//     margin: 15px;
//     width: auto;
//     font-size: 15px;
//   }
</style>