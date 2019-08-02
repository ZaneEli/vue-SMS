<template>
  <div class="customers container">
    <h1 class="page-header">用户管理系统</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th></th>  
        </tr>
      </thead>

      <tbody>
        <tr v-for="customer in customers">
          <td>{{customer.name}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td>
          <td></td>
        </tr>
      </tbody>

    </table>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data () {
    return {
      customers:[]
    }
  },
  methods:{
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users")
          .then(function(response){
            this.customers = response.body;
          })
    }
  },
  created(){
    this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
