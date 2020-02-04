<template>
	<view class="content page">
		<view class="category-text-block" >
			<block v-for="(item,index) in cateTextArray" :key = "index">
				<view class="category-text-content" >
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
				cateTextArray:[]
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
			
			//获取最新产品
			uni.request({
				url: serverUrl+'/wx_CpList_top4.php',
				success: res => {
					this.cateProArray = res.data
					// console.log(res)
				},
			});
		},
		methods: {
			
		},
		
		components:{
			salesProComp
		}
	}
</script>

<style>
	@import url("category.css");

</style>
