<!-- 用户管理系统 -->
<template>
	<div class="customers container">
		<alert v-if="alert" :message="alert"></alert>
		<h1 class="page-header">用户管理系统</h1>
		<input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
		<table class="table table-striped">
			<thead class="center">
				<tr>
					<th>姓名</th>
					<th>年龄</th>
					<th>性别</th>
					<th>电话</th>
					<th>邮箱</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="customer in filterBy(customers,filterInput)">
					<td>{{customer.name}}</td>
					<td>{{customer.age}}</td>
					<td>{{customer.sex}}</td>
					<td>{{customer.phone}}</td>
					<td>{{customer.email}}</td>
					<td>
						<router-link class="btn btn-default" :to="'/detailsPage/'+customer.id">详情</router-link>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
	import alert from './alert'
	
	export default {
		name: 'customers',
		data(){
	  		return{
	  			customers:[],
				alert:"",
				filterInput:""
	  		}
		},
		created(){
			if(this.$route.query){
				this.alert=this.$route.query.alt;
			}
			this.fetchCustomers()
		},
		updated(){
			this.fetchCustomers()
		},
		methods:{
			fetchCustomers(){
				this.$axios
					.get("http://localhost:3000/users")
					.then(response=>{
						this.customers=response.data
					})
			},
			filterBy(customers,value){
				return customers.filter(function(customer){
					return customer.name.match(value);
				})
			}	
		},
		components: {
			alert
		}
	}
</script>

<style scoped>
	#customers{
		
	}
</style>
