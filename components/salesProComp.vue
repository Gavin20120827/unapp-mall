<template name = "salesProComp">

	<navigator class="sales-product-content page-block" url="">
		<image :src="salesArrayImage" mode="widthFix" class="sales-product-image"></image>
		<view class="sales-product-right">
			<view class="sales-product-title">{{salesArrayTitle}}</view>
			<view class="sales-product-desc">产品简介产品简介产品简介产品简介产品简介产品简介产品简介产品简介</view>
			<view class="sales-product-bottom">
				<text class="sales-bottom-num sales-padding">NO.1</text>
				<text class="sales-bottom-people sales-padding"> | 100人付款 | </text>
				<text class="sales-bottom-price sales-padding">¥ {{salesArrayPrice}}</text>
			</view>
		</view>
	</navigator>

</template>

<script>
	export default {
		name: "salesProComp",
		
		data() {
			return {
				
			};
		},
		
		props:{
			salesArrayTitle:0,
			salesArrayImage:0,
			salesArrayPrice:0
		}
	}
</script>

<style>
	.sales-product-content{
		display: flex;
		font-size: 12px;
		align-items: center;
	}
	
	.sales-product-image{
		width: 25%;
		border: 1px solid #fcfafa;
		border-radius: 5px;
		box-shadow: 0px 2px 2px gainsboro;
		padding: 5px;
		margin: 5px;
	}
	
	.sales-product-right{
		width: 70%;
	}
	
	.sales-product-title,.sales-product-desc{
		width: 100%;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	
	.sales-product-title{
		font-size: 12px;
		font-weight: bold;
	}
	
	.sales-product-desc{
		font-size: 10px;
		color: gray;
		padding: 5px 0;
	}
	
	.sales-bottom-num{
		font-size: 10px;
		color: green;
	}
	
	.sales-bottom-people{
		color: gray;
		font-size: 10px;
		margin: 0 5px;
	}
	
	.sales-bottom-price{
		color: red;
	}

</style>
