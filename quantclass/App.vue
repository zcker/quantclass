<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	<style>
		    /*隐藏head标签*/	
		   uni-page-head{display: none;} 
		   /*body高度100%*/
		   uni-page-wrapper{height: 100% !important;}
	</style>
</style>
