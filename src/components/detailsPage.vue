<!-- 详情页 -->
<template>
	<div class="detailsPage container">
		<h1 class="page-header">
			{{customer.name}}
			<span class="pull-right">
				<router-link :to="'/edlit/'+customer.id" class="btn btn-primary">编辑</router-link>
				<button @click="delData(customer.id)" class="btn btn-danger">删除</button>
			</span>
		</h1>
		<ul class="list-group">
			<li class="list-group-item">
				<span class="glyphicon glyphicon-user">{{customer.age}}</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-heart">{{customer.sex}}</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-phone-alt">{{customer.phone}}</span>
			</li>
			<li class="list-group-item">
				<span class="glyphicon glyphicon-envelope">{{customer.email}}</span>
			</li>
		</ul>
	</div>
</template>

<script>
	export default {
		name: 'detailsPage',
		data(){
	  		return{
				customer:""
	  		}
		},
		created(){
			this.fetchCustomers(this.$route.params.id)
		},
		methods:{
			fetchCustomers(id){
				this.$axios
					.get("http://localhost:3000/users/" + id)
					.then(response=>{
						this.customer=response.data;
					})
			},
			delData(id){
				this.$axios
					.delete("http://localhost:3000/users/" + id)
					.then(response=>{
						this.$router.push({path:"/",query:{alt:"用户信息删除成功！"}});
					})
			}
		}
	}
</script>

<style scoped>
	.detailsPage{
		
	}
</style>
