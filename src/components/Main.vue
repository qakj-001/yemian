<template>
  <div>
     <!--导航条 -->
     <nav class="navbar navbar-default">
       <div class="container-fluid">
         <!-- Brand and toggle get grouped for better mobile display -->
         <div class="navbar-header">
           <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
             <span class="sr-only">Toggle navigation</span>
             <span class="icon-bar"></span>
             <span class="icon-bar"></span>
             <span class="icon-bar"></span>
           </button>
           <a class="navbar-brand" href="#">欢迎使用青奥系统</a>
         </div>

         <!-- Collect the nav links, forms, and other content for toggling -->
         <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">


           <ul class="nav navbar-nav navbar-right">

             <li class="dropdown">
               <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">{{user.role==0?"管理员":"普通用户"}}:{{user.username}} <span class="caret"></span></a>
               <ul class="dropdown-menu">
                 <li><a href="javascript:void(0)" @click="toUpdatePwd">更改密码</a></li>
                 <li><a href="javascript:void(0)" @click="logout">登出</a></li>
               </ul>
             </li>
           </ul>
         </div><!-- /.navbar-collapse -->
       </div><!-- /.container-fluid -->
     </nav>

     <div style="width:1170px; margin: 0 auto;">
     <!--左边的内容-->
    <div class="panel-group" id="accordion" role="tablist" aria-multiselectable="true" style="width: 300px; float: left;">
      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="headingOne" >
          <h4 class="panel-title">
            <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
             客户管理
            </a>
          </h4>
        </div>
        <div id="collapseOne" class="panel-collapse collapse in" role="tabpanel" aria-labelledby="headingOne">
          <div class="panel-body" style="padding: 0;">
            <button class="btn btn-default" style="width: 100%;" @click="toCustomer">客户信息</button>
            <button class="btn btn-default" style="width: 100%;" @click="toLinkman">联系人信息</button>
            <button class="btn btn-default" style="width: 100%;">联系记录</button>
          </div>
        </div>
      </div>

      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="headingOne" >
          <h4 class="panel-title">
            <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo" aria-expanded="true" aria-controls="collapseOne">
             供应商管理
            </a>
          </h4>
        </div>
        <div id="collapseTwo" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingOne">
          <div class="panel-body" style="padding: 0;">
            <button class="btn btn-default" style="width: 100%;" @click="toSupplier">供应商信息</button>
            <button class="btn btn-default" style="width: 100%;">检索中心</button>
            <button class="btn btn-default" style="width: 100%;">渠道管理</button>
            <button class="btn btn-default" style="width: 100%;">来电管理</button>
          </div>
        </div>
      </div>

      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="headingOne" >
          <h4 class="panel-title">
            <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseThree" aria-expanded="true" aria-controls="collapseOne">
            商品管理
            </a>
          </h4>
        </div>
        <div id="collapseThree" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingOne">
          <div class="panel-body" style="padding: 0;">
            <button class="btn btn-default" style="width: 100%;">商品信息</button>
            <button class="btn btn-default" style="width: 100%;">采购管理</button>
            <button class="btn btn-default" style="width: 100%;">采购退货</button>
          </div>
        </div>
      </div>


      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="headingOne">
          <h4 class="panel-title">
            <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseFour" aria-expanded="true" aria-controls="collapseOne">
            工作管理
            </a>
          </h4>
        </div>
        <div id="collapseFour" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingOne">
          <div class="panel-body" style="padding: 0;">
            <button class="btn btn-default" style="width: 100%;">日程管理</button>
            <button class="btn btn-default" style="width: 100%;">通讯录</button>
            <button class="btn btn-default" style="width: 100%;">通讯管理</button>
            <button class="btn btn-default" @click="toboard" style="width: 100%;">公告栏</button>
          </div>
        </div>
      </div>

      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="headingOne" >
          <h4 class="panel-title">
            <a role="button" data-toggle="collapse" data-parent="#accordion" href="#collapseFive" aria-expanded="true" aria-controls="collapseOne">
           用户管理
            </a>
          </h4>
        </div>
        <div id="collapseFive" class="panel-collapse collapse" role="tabpanel" aria-labelledby="headingOne">
          <div class="panel-body" style="padding: 0;">
            <button class="btn btn-default" @click="touser()" style="width: 100%;">用户信息</button>
          </div>
        </div>
      </div>
    </div>


     <!--右边的内容-->
     <div style="width: 850px; border: 1px solid #DDDDDD; float: left; margin-left: 10px;">
       <router-view></router-view>
     </div>
    </div>




    </div>
</template>

<script>
  export default{
    data:function(){
      return{
        user:{}
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
      toCustomer:function(){
        this.$router.push("/main/customer");
      },
      toLinkman:function(){
        this.$router.push("/main/linkman");
      },
      logout:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/userController/logout",
          data:{time:new Date().getTime()},
          success:function(result){
            if(result.code == "200"){
              obj.$router.push("/");
            }else{
              alert("操作失败");
            }
          },
          xhrFields: {
            withCredentials: true
          }
        });
      },
      toUpdatePwd:function(){
        this.$router.push("/main/updatePwd");
      },
	  toSupplier:function(){
		  this.$router.push("/main/supplier");
	  },
    toboard:function(){
      this.$router.push("/main/board");
    },
    touser:function(){
      if(this.user.role==0){
        this.$router.push("/main/user");
      }else{
        alert("权限不满足");
      }
    }
    
    
    
    
    
    
    }
  }
</script>

<style scoped>
</style>
