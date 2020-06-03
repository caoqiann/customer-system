<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">添加用户</h1>
    <form v-on:submit="addCustomer">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label>姓名</label>
          <input type="text" class="form-control" placeholder="name" v-model="customer.name">
        </div>
        <div class="form-group">
          <label for="">电话</label>
          <input type="text" class="form-control" placeholder="phone" v-model="customer.phone">
        </div>
        <div class="form-group">
          <label for="">年龄</label>
          <input type="text" class="form-control" placeholder="age" v-model="customer.age">
        </div>
        <div class="form-group">
          <label for="">邮箱</label>
          <input type="text" class="form-control" placeholder="email" v-model="customer.email">
        </div>
        <div class="form-group">
          <label for="">个人简介</label>
<!--          <input type="text" class="form-control" placeholder="profile" v-model="customer.profile">-->
          <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">添加</button>

      </div>
    </form>
  </div>
</template>

<script>
  import Alert from "./Alert";
  export default {
    name: 'add',
    data () {
      return {
        customer: {},
        alert: ""
      }
    },
    methods: {
      addCustomer(e){
        //console.log(123);
        if (!this.customer.name || !this.customer.phone ||!this.customer.email){
          //console.log("请添加对应信息")
          this.alert = "请添加对应信息!"
        }else {
          let newCustomer = {
            //id会自动生成 不用自己写
            name: this.customer.name,
            phone: this.customer.phone,
            email: this.customer.email,
            age: this.customer.age,
            profile: this.customer.profile
          }

          //第二个参数是要传递的数据
          this.$http.post("http://localhost:3000/users",newCustomer)
            .then(function (response) {
             // console.log(response)
              //query是一个对象
              this.$router.push({path:"/", query:{alert:"用户信息添加成功!"}})
            })
        }
        e.preventDefault()
      }

    },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
