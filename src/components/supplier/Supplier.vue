<template>
  <div>
    <button class="btn btn-default" @click="toaddsupplier">添加商家</button><br />
    <table class="table table-bordered">
          <tr>
              <th>商家编号</th>
              <th>商家名字</th>
              <th>商家地址</th>
              <th>商家电话</th>
              <th>商家邮箱</th>
              <th>出售类型</th>
              <th>操作</th>
            </tr>

          <tbody>
            <tr v-for="s in supplier">
              <td>{{s.id}}</td>
              <td>{{s.name}}</td>
              <td>{{s.address}}</td>
              <td>{{s.phone}}</td>
              <td>{{s.email}}</td>
              <td>{{s.type}}</td>
              <td><a href="javascript:void(0)" @click="dele(s.id)"><i class="glyphicon glyphicon-trash"></i></a></td>
              <!-- <td>
                <a href="javascript:void(0)"><i class="glyphicon glyphicon-wrench"></i></a>
                <a href="javascript:void(0)" @click="deleteit()"><i class="glyphicon glyphicon-trash"></i></a>
                <a href="javascript:void(0)" @click="todetails(c.id)"><i class="glyphicon glyphicon-align-justify"></i></a>

              </td> -->
            </tr>
          </tbody>
        </table>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        supplier:[]
      }
    },
    mounted:function(){
      this.getall();
    },
    methods:{
      getall:function(){
        var obj=this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/supplierController/all",
          data:{time:new Date().getTime()},
          success:function(result){
            if(result.code=="200"){
              obj.supplier=result.supplier;
            }else{
              alert("请联系管理员");
            }

          },
          xhrFields: {
            withCredentials: true
          }
        });


      },
      toaddsupplier:function(){
        this.$router.push("/main/insertSupplier");
      },
      dele:function(id){
        var obj=this;
        if(confirm("是否删除？")){
          $.ajax({
            type:"post",
            url:"http://localhost:8082/crm/supplierController/delete/"+id,
            data:{time:new Date().getTime()},
            success:function(result){
               alert(result);
               //重新查询
               obj.getall();
            },
            xhrFields: {
              withCredentials: true
            }
          });
        }



      }



    }



  }
</script>

<style>
</style>
