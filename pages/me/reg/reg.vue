<template>
	<form class="form-block page">
		<view class="form-title">欢迎注册您的账号</view>
		<view class="form-input">
			<input type="text" name="username" value="" class="username form-class" placeholder="请输入账号"/>
			<input type="text" name="password" placeholder="请输入密码" class="password form-class"/>
			<input type="text" name="password" placeholder="请确认您的密码" class="password form-class"/>
			
		</view>
		<view class="form-button-block">
			<view class="form-desc">请正确填写账号信息，有问题联系客服</view>
			<button type="primary" class="form-reg" @click="">注册新用户</button>
		</view>
	</form>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
@import url("reg.css");
</style>
