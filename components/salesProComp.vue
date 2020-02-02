<template name = "salesProComp">

	<view class="sales-product-content page-block">
		<image src="../static/product/cp01.jpg" mode="widthFix" class="sales-product-image"></image>
		<view class="sales-product-right">
			<view class="sales-product-title">中年妈妈装冬季保暖貂绒大衣长款套装</view>
			<view class="sales-product-desc">产品简介产品简介产品简介产品简介产品简介</view>
			<view class="sales-product-bottom">
				<view class="sales-bottom-num sales-padding">NO.1</view>
				<view class="sales-bottom-people sales-padding">100人付款</view>
				<view class="sales-bottom-price sales-padding">¥ 100</view>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		name: "salesProComp",
		
		data() {
			return {
				
			};
		}
	}
</script>

<style>
	.sales-product-content{
		display: flex;
		margin-top: 20upx;
		margin-left: 20upx;
		
	}
	
	.sales-product-right{
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin-left: 20upx;
	}
	
	
	.sales-product-image{
		width:200upx;
	}
	
	.sales-product-title,.sales-product-desc{
		width: 450upx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	
	.sales-product-title{
		font-weight: bold;
	}
	
	.sales-product-desc{
		font-size: 25upx;
	}
	
	.sales-product-bottom{
		display: flex;
		font-size: 30upx;
		
	}
	
	.sales-bottom-price{
		color: red;
	}
	
	.sales-padding{
		padding-right: 20upx;
	}
	
	

</style>
