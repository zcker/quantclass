<template>
	<view class="content">
		<web-view src="https://bbs.quantclass.cn/"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'quantclass'
			}
		},
		onLoad() {
			this.pushHistory() //调用pushHistory方法写入浏览器history当前状态，若不写不能监听到返回popstate方法
			window.addEventListener("popstate", function(e) { //监听手机或浏览器返回按钮 ps：安卓手机需要先点击一下页面此监听才能生效
				if (!window.history.state
					.id) { //t=通过state.id来判断是不是首页 若为首页id值为undefined，但是页面只是url地址发生改变，内容不会转变，所以我这里又重新加载了一遍页面
					window.location.reload()
				} else {
					window.location = 'https://bbs.quantclass.cn/';
				}
			}, false);
		},
		onReady() {
			var that = this;
			uni.getSystemInfo({
				success: function(res) {
					var statusBarHeight = res.statusBarHeight;
					var screenHeight = res.screenHeight;
					var webviewHeight = screenHeight - statusBarHeight;
					that.$scope.$getAppWebview().children()[0].setStyle({
						top: statusBarHeight + 'px',
						height: webviewHeight + 'px'
					})
				}
			})
		},
		onBackPress(event) {
			var that = this;
			that.$scope.$getAppWebview().children()[0].canBack(function(e) {
				console.log(e);
				if (e.canBack == true) {
					that.$scope.$getAppWebview().children()[0].back();
					return true;
				} else {
					let main = plus.android.runtimeMainActivity();
					main.moveTaskToBack();
				}
			})
		},
		methods: {
			pushHistory() {
				var state = {
					title: "title",
					url: "#"
				};
				window.history.pushState(state, "title", "#"); //往history对象写入状态
			},
		}
	}
</script>

<style>

</style>
