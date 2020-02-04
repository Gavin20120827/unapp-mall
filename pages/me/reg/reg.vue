<template>
	<form class="form-block page" @submit="formSubmit">
		<view class="form-title">欢迎注册您的账号</view>
		<view class="form-input">
			<input type="text" name="username" value="" class="username form-class" placeholder="请输入账号"/>
			<input password type="text" name="password" placeholder="请输入密码" class="password form-class"/>
			<input password type="text" name="psd" placeholder="请确认您的密码" class="password form-class"/>
		</view>
		
		<view class="form-button-block">
			<view class="form-desc">请正确填写账号信息，有问题联系客服</view>
			<view v-if="form_error != ''" class="form-error">{{form_error}}</view>
			<button type="primary" class="form-reg" form-type="submit">注册新用户</button>
		</view>
		
	</form>
</template>

<script>
	import common from "../../../common/common.js";
	
	export default {
		
		data() {
			return {
				form_error:""
			}
		},
		methods: {
			//用户注册流程
			formSubmit:function(e){
				var serverUrl = common.serverUrl
				var username = e.detail.value.username
				var password = e.detail.value.password
				var psd = e.detail.value.psd
				
				if(username !='' & password !=''){
					if(username.length >= 2 & password.length >=6){
						if(password === psd){
							this.form_error = ''
								
								//把数据写入服务器，并且返回是否成功
								uni.request({
									url: serverUrl+'/wx_check_reg_yonghu.php',
									method: 'GET',
									data: {
										yhm: username,
										mm: password
									},
									success: res => {
										// console.log(res.data)
										if(res.data.zt == 'yes'){
											
											//写入数据库成功，再写入缓存
											uni.setStorage({
											    key: 'u_login',
											    data: 'ok',
											    success: function () {
											        console.log('u_login写入缓存');
											    }
											});
											
											uni.setStorage({
											    key: 'u_id',
											    data: res.data.uid,
											});
											
											uni.setStorage({
											    key: 'username',
											    data: username,
											    success: function () {
											        // 注册成功，跳转用户中心
											        uni.switchTab({
											        	url: '/pages/me/me'
											        });
											    }
											});
											
										}else if(res.data.zt == 'no'){
											var form_error = '注册失败:'+ res.data.xinxi
											this.form_error = form_error
										}
									}
								});
							
						}else{
							var form_error = "两次密码输入不一致"
							this.form_error = form_error
						}
					}else{
						var form_error = "账号密码长度不对"
						this.form_error = form_error
					}
				}else{
					var form_error = "账号或者密码不能为空"
					this.form_error = form_error
				}
			}
	
		}
	}
</script>

<style>
@import url("reg.css");
</style>
