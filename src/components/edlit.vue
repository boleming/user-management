<!-- 编辑 -->
<template>
	<div class="edlit container">
		<alert v-if="alert" :message="alert"></alert>
		<h1 class="page-header">编辑信息</h1>
		<form @submit.prevent="edlitCustomer">
			<div class="well">
				<h4>用户信息</h4>
				<div class="form-group">
					<label>姓名</label>
					<input type="text" class="form-contr" placeholder="name" v-model="customer.name">
				</div>
				<div class="form-group">
					<label>电话</label>
					<input type="text" class="form-contr" placeholder="phone" v-model="customer.phone">
				</div>
				<div class="form-group">
					<label>邮箱</label>
					<input type="text" class="form-contr" placeholder="email" v-model="customer.email">
				</div>
				<div class="form-group">
					<label>性别</label>
					<input type="text" class="form-contr" placeholder="sex" v-model="customer.sex">
				</div>
				<div class="form-group">
					<label>年龄</label>
					<input type="text" class="form-contr" placeholder="age" v-model="customer.age">
				</div>
				<button type="submit"  class="btn btn-primary">编辑</button>
			</div>
		</form>
	</div>
</template>

<script>
	export default {
		name: 'edlit',
		data(){
	  		return{
	  			customer:{},
				alert:""
	  		}
		},
		created(){
			this.fetchCustomers()
		},
		methods:{
			edlitCustomer(){
				if(!this.customer.name || !this.customer.phone || !this.customer.email || !this.customer.sex || !this.customer.age){
					alert("请填写对应信息");
				}else{
					let newCustomer={
						name:this.customer.name,
						phone:this.customer.phone,
						email:this.customer.email,
						sex:this.customer.sex,
						age:this.customer.age
					}
					this.$axios
						.put("http://localhost:3000/users/" + this.$route.params.id,newCustomer)
						.then(response=>{
							this.$router.push({path:"/",query:{alt:"用户信息编辑成功！"}});
						})
				}
			},
			fetchCustomers(){
				this.$axios
					.get("http://localhost:3000/users/" + this.$route.params.id)
					.then(response=>{
						this.customer=response.data;
					})
			}
		},
		components: {
			alert
		}
	}
</script>

<style scoped>
	#edlit{
		
	}
</style>
