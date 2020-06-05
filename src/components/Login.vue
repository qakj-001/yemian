<template>
  <div class="login">
      <div class="center">
          <h1><img src="../assets/img/Windows10.png" alt=""></h1>

              <div class="inputLi">
                  <input type="text" class="user" placeholder="请输入" required v-model="username">
              </div>
              <div class="inputLi">
                  <input type="password" class="pwd" placeholder="请输入" required v-model="password">
              </div>
              <div class="inputLi">
                  <button @click="login">登录</button>
              </div>
          <p class="tip">欢迎使用青奥科技管理系统</p>
      </div>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        username:"",
        password:"",

      }
    },
    methods:{
      login:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/userController/login",
          data:{time:new Date().getTime(),username:obj.username,password:obj.password},
          success:function(result){
            if(result.code == "200"){
              obj.$router.push("/main/customer");
            }else{
              alert(result.msg);
            }
          },
          xhrFields: {
                      withCredentials: true
                    }
        });
      }
    }
  }
</script>

<style scoped>
  @import url("../assets/css/login.css");
</style>
