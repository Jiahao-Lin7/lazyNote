<template>
    <div class="bg">
    <div class="container">
      <div class="login">
        <div class="logo">
          <h3>Lazy   Note</h3>
        </div>
        <div class="login-input">
          <el-form
            :model="ruleForm"
            status-icon
            :rules="rules"
            ref="ruleForm"
            class="demo-ruleForm"
          >
            <el-form-item label="" prop="email">
              <el-input
                v-model="ruleForm.email"
                clearable
                placeholder="邮箱"
              ></el-input>
            </el-form-item>
            <el-form-item label="" prop="pass">
              <el-input
                type="password"
                v-model="ruleForm.pass"
                autocomplete="off"
                placeholder="密码"
                clearable
              ></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submitForm('ruleForm')">
                <loading v-if="load"></loading>
                <span v-else>登录</span>
              </el-button>
            </el-form-item>
          </el-form>
          <p class="register">
            <router-link to="/register">还没有账号？注册</router-link>
          </p>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
import loading from "../components/loading";
export default {
  name: "login",
  components: { loading },
  data() {
    var checkEmail = (rule, value, callback) => {
      var reg = new RegExp(
        "^[a-z0-9]+([._\\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$"
      );
      if (!value) {
        return callback(new Error("邮箱不能为空"));
      }
      setTimeout(() => {
        if (!reg.test(value)) {
          callback(new Error("请输入正确的邮箱"));
        } else {
          callback();
        }
      }, 1000);
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    return {
      load: false,
      ruleForm: {
        pass: "",
        email: "",
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        email: [{ validator: checkEmail, trigger: "blur" }],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.load = true;
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$router.push({
            name:'index'
        })
          // this.$api.user
          //   .login({
          //     email: this.ruleForm.email,
          //     password: this.ruleForm.pass,
          //   })
          //   .then(({ data }) => {
          //     this.load = false;
          //     if (data.status == "0") {
          //       this.$store.dispatch("UserLogin", data.result.token);
          //       this.$store.dispatch("UserName", data.result.email);
          //       let redirect = decodeURIComponent(
          //         this.$route.query.redirect || "/"
          //       );
          //       this.$router.push({
          //         name:'index'
          //       });
          //     } else {
          //       this.$message.error(data.msg);
          //     }
          //   });
        } else {
          alert("请输入正确的邮箱地址与密码!!");
          return false;
        }
      });
    },
  },
};
</script>

<style lang='scss'>
.bg{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  // background: url('../common/img/1.jpg') no-repeat;
  // background-size: cover;
}
.container {
  width: 25%;
  height: 60%;
  margin-top: -10%;
}
.login {
  width: 100%;
  height: 100%;
  background: #db4c3f;
  border: 2px #db4c3f solid;
  opacity: 0.4;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  .logo {
    color:rgb(163, 63, 38) !important;
    font-size: 30px;
    // font-style: italic;
    font-weight: bold;
    margin-bottom: 20px;
    h3 {
      margin: 0 !important;
      font-size: 200% !important;
    }
  }
  .login-input {
    width: 80%;
    padding: 10px;
    margin-top: 10px;
    .el-input {
      // margin-bottom: 20px;
      .el-input__inner {
        border-radius: 30px !important;
        text-align: center;
      }
    }
    .el-button {
      border-radius: 30px !important;
      width: 100% !important;
      text-align: center;
      background: #cf6c63 !important;
      color: rgb(233, 231, 229) !important;
      border: 0;
    }
    .register {
      text-align: right;
      margin: 10px;
      a {
        color: #fafafa !important;
      }
    }
  }
}
</style>