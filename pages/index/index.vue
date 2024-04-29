<template>
	<view>
		<div v-for="site in urls" :key="site.name" style="font-size: 30px; padding: 30px;" @click="openUrl(site.url)">
			{{ site.name }}
		</div>
		<web-view class="web" v-if="selectedUrl" :src="selectedUrl" @message="onMessage">
			<cover-view class="cover" back-button-events="true">
				<cover-view class="button_box" @click="goBack">
					返回
				</cover-view>
			</cover-view>
		</web-view>
	</view>
</template>

<script>
	import urls from "../../data/urls.json";

	export default {
		data() {
			return {
				urls: [], // 保存 JSON 文件中的数据
				selectedUrl: null, // 用户点击的 URL
			};
		},
		methods: {
			onMessage(e) {
				// 处理来自 web-view 的消息
				console.log(e);
			},
			openUrl(url) {
				// 用户点击时更新 selectedUrl，触发 WebView 的显示
				this.selectedUrl = url;
			},
			goBack() {
				this.selectedUrl = null;
			},
		},
		mounted() {
			// 将导入的 JSON 数据保存到组件的数据中
			this.urls = urls.urls;
		},
	};
</script>

<style>
	.cover {
		/* width: 100px;
		height: 100px;
		background-color: #000;
		position: relative; */
		position: fixed;
		bottom: 50px;
		right: 5px;
		z-index: 999999999;
		transform: translateX(-50%);
	}



	.button_box {
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		border-radius: 8px;
		width: 50px;
		color: black;
		background-color: #dadada;
		opacity: 0.6;
		padding: 10px;
		/* position: absolute;
		top:0;
		left:0;
		right:0;
		bottom:0;
		margin: auto;
		width:50px ;
		height: 50px; */
	}
</style>