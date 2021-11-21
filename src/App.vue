<template>
  <div>
    <form v-if="!isReg">
      <div>用户名:</div>
      <input type="text" v-model="name">
      <div>密码:</div>
      <input type="password" v-model="password">
      <button type="button" @click="login()">登录</button>
      <button type="button" @click="reg()">注册</button>
    </form>
    <form v-else>
      <div>用户名:</div>
      <input type="text" v-model="name">
      <div>密码:</div>
      <input type="password" v-model="password">
      <div>再次输入密码:</div>
      <input type="password" v-model="repeat">
      <button type="button" @click="addUser()">确定</button>
      <button type="button" @click="cancel()">取消</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      isReg: false,
      name: "",
      password: "",
      repeat: ""
    };
  },
  methods: {
    login() {
      //验证姓名和密码是否与locastorage一致
      if (
          localStorage.getItem("name") === this.name &&
          localStorage.getItem("password") === this.password
      ) {
        //清空输入框
        this.name = "";
        this.password = "";
        // this.$router.push("/home/list");
        this.push("/home/list");
      } else {
        alert('用户名或密码不正确');
      }
    },
    reg() {
      this.isReg = true;
    },
    cancel() {
      this.isReg = false;
    },
    addUser() {
      //验证两次输入密码是否一致
      if (this.password === this.repeat) {
        //将名字和密码存入localstorage中
        localStorage.setItem("name", this.name);
        localStorage.setItem("password", this.password);
        //清空输入框
        this.name = "";
        this.password = "";
        this.isReg = false;
      } else {
        alert("两次密码不一致");
      }
    }
  }
};
</script>
<!--

<style scoped>
</style>-->
