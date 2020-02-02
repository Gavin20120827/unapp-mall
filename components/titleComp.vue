<template name = "titleComp">
	<view class="Newest-title-block">
		<view class="Newest-title-left">{{titleCompText}}</view>
		<view class="Newest-title-right">
			<view class="Newest-title-right-test">更多</view>
			<image src="../static/news/right.png" class="Newest-title-image" mode="widthFix"></image>
		</view>
	</view>
</template>

<script>
	export default {
		name: "titleComp",
		
		data() {
			return {
				
			};
		},
		
		props:{
			titleCompText:0,
		}
	}
</script>

<style>
	/* 最新产品标题开始 */
	.Newest-title-block{
		display: flex;
		justify-content: space-between;
		background-color: #F0AD4E;
		padding: 10upx;
		font-size:40upx;
		height: 60upx;
	}
	
	.Newest-title-left{
		margin-left: 20upx;
		border-left: 5px solid red;
		padding-left: 20upx;
	}
	
	.Newest-title-right{
		display: flex;
		padding-right: 20upx;
	}
	
	.Newest-title-image{
		width: 50upx;
		padding-top: 5upx;
	}
	/* 最新产品标题结束 */

</style>
