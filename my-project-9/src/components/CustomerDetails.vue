<!-- 用户详情显示界面 -->
<template>
	<div class="details container">
		<router-link to="/" class="btn btn-default">返回</router-link>
		<h1 class="page-header">
			{{customer.name}}
			<span class="pull-right">
				<router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
					编辑
				</router-link>
				<button class="btn btn-info" v-on:click="exportToExcel(customer.id)">
					导出
				</button>
				<button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">
					删除
				</button>
			</span>
		</h1>
		<!-- 显示用户的信息 span标签中是图标 https://www.bootcss.com/ 组件中查找图标信息 -->

		<ul class="list-group">
			<li class="list-group-item">
				<span class="glyphicon glyphicon-phone"> 
					{{customer.phone}}
				</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-envelope">
					{{customer.email}}
				</span>
			</li>
		</ul>

		<ul class="list-group">
			<li class="list-group-item">
				<span class="glyphicon glyphicon-home"> 
					{{customer.education}}
				</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-home">
					{{customer.graduationschool}}
				</span>
			</li>     	
			<li class="list-group-item">
				<span class="glyphicon glyphicon-home">
					{{customer.profession}}
				</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-home">
					{{customer.profile}}
				</span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'customerdetails',
	data () {
		return {
			customer:""
		}
	},
	methods:{
		fetchCustomers(id){
			this.$http.get("http://localhost:3000/users/"+id)
				.then(function(response){
          			// console.log(response);
          			this.customer = response.body;
          		})
		},
		deleteCustomer(id){
			console.log(id);
			this.$http.delete("http://localhost:3000/users/"+id)
				.then(function(response){
					this.$router.push({path:"/",query:{alert:"用户信息删除成功"}});	
			}) 
		},

		exportToExcel(id){
			this.$http.get("http://localhost:3000/users/"+id)
				.then(function(response){
          			console.log(response);          			
          		})
			
　 		}
	},
    formatJson(filterVal, jsonData) {
        return jsonData.map(v => filterVal.map(j => v[j]))
		
	},
	created(){
		this.fetchCustomers(this.$route.params.id);
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
