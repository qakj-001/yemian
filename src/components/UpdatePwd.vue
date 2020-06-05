<template>
  <div>
      <div class="form-horizontal">
        <div class="form-group">
          <label  class="col-sm-2 control-label">原密码</label>
          <div class="col-sm-10">
            <input type="email" class="form-control" placeholder="请输入原密码" v-model="oldPwd">
          </div>
        </div>

        <div class="form-group">
          <label  class="col-sm-2 control-label">新密码</label>
          <div class="col-sm-10">
            <input type="email" class="form-control" placeholder="请输入新密码" v-model="newPwd">
          </div>
        </div>

        <div class="form-group">
          <label  class="col-sm-2 control-label">确认密码</label>
          <div class="col-sm-10">
            <input type="email" class="form-control" placeholder="请输入确认密码" v-model="newPwd2">
          </div>
        </div>
        <button class="btn btn-default" style="margin-left: 400px;" @click="comfirm">确认修改</button>
      </div>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        oldPwd:"",
        newPwd:"",
        newPwd2:""
      }
    },
    mounted:function(){
      this.getUser();
    },
    methods:{
      getUser:function(){
          var obj = this;
          $.ajax({
              type:"post",
              url:"http://localhost:8082/crm/userController/user",
              data:{time:new Date().getTime()},
              success:function(result){
                 if(result.code == "200"){
                     obj.user = result.user;
                  }else{
                    obj.$router.push("/");
                  }
              },
              xhrFields: {
                withCredentials: true
              }
          });
      },
      comfirm:function(){
        if(this.oldPwd!=this.user.password){
          alert("输入原密码错误");
          return;
        }
        if(this.newPwd!=this.newPwd2){
          alert("两次密码不一致");
          return;
        }

        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/userController/updatePwd",
          data:{time:new Date().getTime(),id:obj.user.id,password:obj.newPwd},
          success:function(result){
             if(result == "200"){
                 alert("修改成功");
              }else{
                alert("修改失败");
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

<style>
</style>
