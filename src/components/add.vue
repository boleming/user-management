<!-- 添加 -->
<template>
	<div class="add container">
		<alert v-if="alert" :message="alert"></alert>
		<h1 class="page-header">添加用户</h1>
		<form @submit.prevent="addCustomer">
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
				<button type="submit"  class="btn btn-primary">添加</button>
			</div>
		</form>
	</div>
</template>

<script>
	import alert from './alert'
	
	export default {
		name: 'add',
		data(){
	  		return{
	  			customer:{},
				alert:""
	  		}
		},
		methods:{
			addCustomer(){
				if(!this.customer.name || !this.customer.phone || !this.customer.email || !this.customer.sex || !this.customer.age){
					this.alert="请填写对应信息";
				}else{
					let newCustomer={
						name:this.customer.name,
						phone:this.customer.phone,
						email:this.customer.email,
						sex:this.customer.sex,
						age:this.customer.age
					}
					this.$axios
						.post("http://localhost:3000/users",newCustomer)
						.then(response=>{
							this.$router.push({path:"/",query:{alt:"用户信息添加成功！"}});
						})
				}
			}
		},
		components: {
			alert
		}
	}
</script>

<style scoped>
	#add{
		
	}
</style>
