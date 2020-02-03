<template>
	<view class="content page">
		<!-- 轮播图开始 -->
		<swiper :indicator-dots="true" :autoplay="true" class="swiper-block">
			<block v-for="(item,index) in swiperImageSrc" :key="index">
				<swiper-item class="swiper-single">
					<image class="swiper-image" :src="item.tupian" mode="widthFix"></image>
				</swiper-item>
			</block>
		</swiper>
		<!-- 轮播图结束 -->
		
		<!-- 菜单开始 -->
		<view class="menu-block page-block">
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu01.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">品牌大全</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu02.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">最新上架</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu03.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">用户中心</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu04.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">订单列表</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu05.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">留言反馈</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu06.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">活动列表</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu07.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">帮助中心</view>
			</navigator>
			<navigator url="" class="menu-content">
					<image src="../../static/menu/menu08.png" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">关于我们</view>
			</navigator>
		</view>
		<!-- 菜单结束 -->
		
		<!-- 资讯开始 -->
		<block v-for="(item,index) in newsArray" :key="index">
			<navigator class="news-block page-block" :url="item.myid">
				<image src="../../static/news/news.png" class="news-image news-content" mode="widthFix"></image>
				<view class="news-title news-content">{{item.myshijian}} {{item.mybiaoti}}</view>
				<image src="../../static/news/right.png" class="news-image-right" mode="widthFix"></image>
			</navigator>
		</block>
		<!-- 资讯结束 -->
				
		<!-- 最新产品开始 -->
		<view class="Newest-product-block page-block">
			<!-- 最新产品标题开始 -->
			<titleComp :titleCompText = "titleCompText"></titleComp>				
			<!-- 最新产品标题结束 -->
			
			<!-- 最新产品内容开始 -->
			<view class="Newest-product-content-block">
				<block v-for="(item,index) in newestProduct" :key="index">
					<navigator class="Newest-product-content" url="">
						<image :src="item.cp_tupian" mode="widthFix" class="Newest-product-image"></image>
						<view class="Newest-product-title">{{item.cp_mingcheng}}</view>
						<view class="Newest-product-price">
							<text class="Newest-price-num">¥ {{item.jiage}}</text>
							<text class="Newest-price-text">100人付款</text>
						</view>
					</navigator>
				</block>
			</view>
			<!-- 最新产品内容结束 -->
		</view>
		<!-- 最新产品结束 -->
		
		<!-- 销售排行开始 -->
		<view class="sales-product-block">
			<!-- 销售排行标题开始 -->
			<titleComp :titleCompText = "titleCompText"></titleComp>
			<!-- 销售排行标题结束 -->
			
			<!-- 销售排行内容开始 -->
			<block v-for="(item,index) in salesArray" :key = "index">
				<salesProComp :salesArrayTitle = "item.cp_mingcheng" :salesArrayImage="item.cp_tupian" :salesArrayPrice="item.jiage"></salesProComp>
			</block>
			<!-- 销售排行内容结束 -->
		</view>
		<!-- 销售排行结束 -->
		

	</view>
</template>

<script>
	import titleComp from "../../components/titleComp.vue";
	import salesProComp from "../../components/salesProComp.vue";
	import common from "../../common/common.js";
	
	export default {
		data() {
			return {
				swiperImageSrc:[],
				newsArray:[],
				newestProduct:[],
				titleCompText:"最新产品",
				salesArray:[]
			}
		},
		onLoad() {
			var serverUrl = common.serverUrl;
			
			// 获取轮播图片
			uni.request({
				url: serverUrl+'/wx_lunbo.php',
				success: res => {
					if(res.statusCode == 200){
						var swiperImageSrc = res.data
						this.swiperImageSrc = swiperImageSrc;
						// console.log(res.data);
						};
				}
			});
			
			//获取新闻资讯
			uni.request({
				url: serverUrl+'/wx_news_list.php',
				success: res => {
					var newsArray = res.data
					this.newsArray = newsArray
					// console.log(newsArray)
				},
			});
			
			//获取最新产品
			uni.request({
				url: serverUrl+'/wx_CpList_top4.php',
				success: res => {
					var newestProduct = res.data
					this.newestProduct = newestProduct
					// console.log(res)
				},
			});
			
			//获取销售排行数据
			uni.request({
				url: serverUrl+'/wx_CpList_top4.php',
				success: res => {
					var salesArray = res.data
					this.salesArray = salesArray
					console.log(res);
				}
			});

		},
		methods: {

		},
		
		components:{
			titleComp,
			salesProComp
		}
	}
</script>

<style>
  @import url("index.css");
</style>
