<template>
  <div>
    <h2>客户详情</h2>
        客户编号：{{customer.id}}<br />
        客户名字:{{customer.name}}<br />
        客户性别:{{customer.sex == 0?"男":"女"}}<br />
        客户电话:{{customer.phone}}<br />
        客户生日:{{customer.birth}}<br />
        <a href="javascript:void(0)" @click="goback()">返回...</a>
  </div>
</template>

<script>
  export default{
    data:function(){
      return{
        id:this.$route.query.id,
        customer:{}
      }
    },
    mounted:function(){
      this.getDetails();
    },
    methods:{
      goback:function(){
        this.$router.go(-1);
      },
      getDetails:function(){
        var obj = this;
        $.ajax({
          type:"post",
          url:"http://localhost:8082/crm/customerController/getDetails",
          data:{time:new Date().getTime(),id:obj.id},
          success:function(result){
              if(result.code == "200"){
                  obj.customer =  result.data;
              }else{
                  alert("有问题，请联系管理员");
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
