<template name = "titleComp">
	<view class="Newest-title-block">
		<view class="Newest-title-border"></view>
		<view class="Newest-title-left">{{titleCompText}}</view>
		<view class="Newest-title-right">更多></view>
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
		align-items: center;
		background-color: aliceblue;
	}
	
	.Newest-title-border{
		width: 3px;
		height: 18px;
		background-color: green;
		margin: 5px;
		box-shadow: 2px 2px 2px gainsboro;
	}
	
	.Newest-title-left{
		flex-grow: 1;
		color: gray;
		text-shadow: 1px 1px 1px gainsboro;
	}
	
	.Newest-title-right{
		margin-right: 5px;
		color: gray;
		text-shadow: 2px 2px 2px gainsboro;
	}
	/* 最新产品标题结束 */

</style>
