<template>
  <div>
    <h3>添加信息</h3>
    <form class="form-horizontal" style="margin-left: -33px; width: 800px;">

      <div class="form-group">
        <label for="inputEmail3" class="col-sm-2 control-label">名字</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" v-model="supplier.name">
        </div>
      </div>

      <div class="form-group">
        <label for="inputEmail3" class="col-sm-2 control-label">地址</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" v-model="supplier.address">
        </div>
      </div>

      <div class="form-group">
        <label for="inputEmail3" class="col-sm-2 control-label">电话</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" v-model="supplier.phone">
        </div>
      </div>
      <div class="form-group">
        <label for="inputPassword3" class="col-sm-2 control-label">邮箱</label>
        <div class="col-sm-10">
          <input type="email" class="form-control" v-model="supplier.email">
        </div>
      </div>

      <div class="form-group">
        <label for="inputEmail3" class="col-sm-2 control-label">出售款式</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" v-model="supplier.type">
        </div>
      </div>

      <div class="form-group">
        <div class="col-sm-offset-2 col-sm-10">
          <button type="submit" @click="add()" class="btn btn-default">添加</button>
        </div>
      </div>
    </form>


  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        supplier:{name:"",address:'',phone:"",email:"",type:""}
      }
    },

    methods:{
      add:function(){
        var obj=this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/supplierController/add",
          data:{time:new Date().getTime(),name:obj.supplier.name,address:obj.supplier.address,phone:obj.supplier.phone,email:obj.supplier.email,type:obj.supplier.type},
          success:function(result){
            alert(result);
            obj.$router.push("/main/supplier");
          },
           xhrFields: {
                      withCredentials: true
            }

        })
      }




    }




  }
</script>

<style>
</style>
