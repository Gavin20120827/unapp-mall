<template>
	<view class="content page">
		<view class="category-text-block" >
			<block v-for="(item,index) in cateTextArray" :key = "index">
				<view class="category-text-content " :class="checkCategory ==item.id ? 'checkColor' : '' " :data-id ="item.id" @click="categoryId">
					{{item.name}}
				</view>
			</block>
		</view>
		<view class="category-product-block page-block">
			<block v-for="(item,index) in cateProArray" :key = "index">
				<salesProComp :salesArrayTitle = "item.cp_mingcheng" :salesArrayImage="item.cp_tupian" :salesArrayPrice="item.jiage"></salesProComp>
			</block>
		</view>
		
		
	</view>
</template>

<script>
	import salesProComp from "../../components/salesProComp.vue"
	import common from "../../common/common.js"
	
	export default {
		data() {
			return {
				cateProArray:[],
				cateTextArray:[],
				checkCategory:''
			}
		},
		onLoad() {
			var serverUrl = common.serverUrl
			//获取左侧分类
			uni.request({
				url: serverUrl+'/wx_fenlei.php',
				success: res => {
					this.cateTextArray = res.data
				}
			});
			
			//默认加载第一个分类的产品
			uni.request({
				url:serverUrl+"/wx_fenlei_chanpin.php",
				data:{
					//241是第一个分类的ID
				    int_lxid1:241
				},
				success: res => {
					this.cateProArray = res.data
					// console.log(res.data)
				},
			});
		},
		
		methods: {
			// 点击左侧分类切换右边的商品
			categoryId:function(e){
				var serverUrl = common.serverUrl
				var checkCategory = e.target.dataset.id
				this.checkCategory = checkCategory
				// console.log(e.target.dataset.id)
				
				//根据ID获取右侧的产品
				uni.request({
					url:serverUrl+"/wx_fenlei_chanpin.php",
					data:{
					    int_lxid1:checkCategory
					},
					success: res => {
						this.cateProArray = res.data
						// console.log(res.data)
					},
				});
			}
		},
		
		components:{
			salesProComp
		}
	}
</script>

<style>
	@import url("category.css");

</style>
