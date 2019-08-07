<!-- 用户详情显示界面  -->
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
	
		<table data="tabledata" class="table table-striped table-hover">
			<thead>
				<th width="200"> 类别</th>
				<th width="300"> info</th>
				<th width='400'> 备注</th>
			</thead>
      	<tbody>
	        <tr>
	        	<th>电话</th>
	        	<td>{{customer.phone}}</td>
	        	<td></td>
	        </tr>
	        <tr>
	        	<th>邮箱</th>
		        <td>{{customer.email}}</td>
		        <td></td>	        
	        </tr>
	        <tr>
	        	<th>学历</th>
		        <td>{{customer.education}}</td>
		        <td></td>	  
	        </tr>
	        <tr>
	        	<th>毕业学校</th>
		        <td>{{customer.grauationschool}}</td>
		        <td></td>	  
	        </tr>
	        <tr>
	        	<th>专业</th>
		        <td>{{customer.profession}}</td>
		        <td></td>	  
	        </tr>
	        <tr>
	        	<th>备注</th>
		        <td>{{customer.profile}}</td>
		        <td></td>	  
	        </tr>
      	</tbody>
    </table>

		<!-- <ul class="list-group">
			<li class="list-group-item">
				<span class="glyphicon glyphicon-phone"> 	
					显示用户的信息 span标签中是图标 https://www.bootcss.com/ 组件中查找图标信息
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
		</ul> -->
	</div>
		

</template>

<script>
export default {

	name: 'customerdetails',
	data () {
		return {
			customer:"",
			list:[
			{				
				name:"fun",
				phone:"1230",
				id:100,	
			},
			{
				name:"fun2",
				phone:"113",
				id:99,	
			}
			],
			lists:[]
		}
	},
	methods:{
		fetchCustomers(id){
			this.$http.get("http://localhost:3000/users/"+id)
				.then(function(response){
          			//console.log(response);
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
			/*this.$http.get("http://localhost:3000/users/"+id)
				.then(function(response){
          			///var list=response.bodyText;
          			console.log(this.customer);
          			this.lists.push(this.customer);
          			console.log(this.lists);
          			console.log(this.list);
          			
		         
          			require.ensure([],()=>{
	          			const{export_json_to_excel}=require('../vendor/Export2Excel'); //引入文件
		          		const tHeader = ["姓名","手机号","邮箱","学历","毕业学校","专业","备注"]; //将对应的属性名转入
		          		const filterVal=["name","phone","email","education","graduationschool","profession","profile"];	          	
		          		const data = this.formatJson(filterVal, this.lists);
		          		export_json_to_excel(tHeader,data,'model');
	          			})       			
          		})*/
          	this.lists.push(this.customer);
         	require.ensure([],()=>{
	          		const{export_json_to_excel}=require('../vendor/Export2Excel'); //引入文件
	          		const tHeader =["姓名","手机号","邮箱","学历","毕业学校","专业","备注"]; //将对应的属性名转入
	          		const filterVal=["name","phone","email","education","graduationschool","profession","profile"];
	          		//this.lists 为一个数组中包含json	          		
	          		const data = this.formatJson(filterVal, this.lists);	          	
	          		export_json_to_excel(tHeader,data,'model');
          		})
            },
        formatJson(filterVal, jsonData) {
        	return jsonData.map(v => filterVal.map(j => v[j]))
      		}    
		},
	created(){
			this.fetchCustomers(this.$route.params.id);
		}
	
	}
</script>

/*Add "scoped" attribute to limit CSS to this component only */


<style scoped>

</style>
