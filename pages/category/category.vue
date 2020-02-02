<template>
	<view class="content page">
		<view class="category-text-block" >
			<block v-for="(item,index) in cateTextArray" :key = "index">
				<view class="category-text-content">
					Web前端
				</view>
			</block>
		</view>
		<view class="category-product-block page-block">
			<block v-for="(item,index) in cateProArray" :key = "index">
				<salesProComp></salesProComp>
			</block>
		</view>
		
		
	</view>
</template>

<script>
	import salesProComp from "../../components/salesProComp.vue";
	
	export default {
		data() {
			return {
				cateProArray:[1,2,3,4,5,6],
				cateTextArray:[1,2,3,4,5,6],
			}
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
