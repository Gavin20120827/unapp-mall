<template>
	<view class="content page">
		<!-- 轮播图开始 -->
		<swiper :indicator-dots="true" :autoplay="true" class="swiper-block">
			<block v-for="(item,index) in swiperArray" :key="index">
				<swiper-item class="swiper-single">
					<image class="swiper-image" :src="swiperImageSrc" mode="widthFix"></image>
				</swiper-item>
			</block>
		</swiper>
		<!-- 轮播图结束 -->
		
		<!-- 菜单开始 -->
		<view class="menu-block page-block">
			<block v-for="(item,index) in menuArray" :key="index">
				<view class="menu-content">
					<image :src="menuImageSrc" class="menu-image" mode="widthFix"></image>
					<view class="menu-text">{{menuText}}</view>
				</view>
			</block>
		</view>
		<!-- 菜单结束 -->
		
		<!-- 资讯开始 -->
		<block v-for="(item,index) in newsArray" :key="index">
			<view class="news-block page-block">
					<view class="news-content-left">
						<image src="../../static/news/news.png" class="news-image news-content" mode="widthFix"></image>
						<view class="news-date news-content">2020-02-01</view>
						<view class="news-title news-content">
							网上商城功能概要网上商城功能概要
						</view>
					</view>
					<view class="news-content-right">
						<image src="../../static/news/right.png" class="news-image-right" mode="widthFix"></image>
					</view>
			</view>
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
					<view class="Newest-product-content">
						<image src="../../static/product/cp01.jpg" mode="widthFix" class="Newest-product-image"></image>
						<view class="Newest-product-title">中年妈妈装冬季保暖貂绒大衣长款套装</view>
						<view class="Newest-product-price">
							<view class="Newest-price-text">价格：</view>
							<view class="Newest-price-num">¥ 100</view>
						</view>
					</view>
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
				<salesProComp></salesProComp>
			</block>
			<!-- 销售排行内容结束 -->
		</view>
		<!-- 销售排行结束 -->
		

	</view>
</template>

<script>
	import titleComp from "../../components/titleComp.vue";
	import salesProComp from "../../components/salesProComp.vue";
	
	export default {
		data() {
			return {
				swiperArray: [1,2],
				swiperImageSrc:'../../static/swiper/batmanvssuperman.png',
				menuArray:[1,2,3,4,5,6,7,8],
				menuImageSrc:"../../static/menu/menu01.png",
				menuText:"所有产品",
				newsArray:[1,2,3,4],
				newestProduct:[1,2,3,4,5,6,7,8],
				titleCompText:"最新产品",
				salesArray:[1,2,3,4,5]
			}
		},
		onLoad() {

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
