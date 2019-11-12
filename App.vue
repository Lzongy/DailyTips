<script>
	export default {
		onLaunch: function() {
			console.log('App已安装')
		},
		onShow: function() {
			console.log('App已运行')
		},
		onHide: function() {
			console.log('关闭App')
		},
		onError:function(){
			uAlert('页面出错')
		}
	}
</script>

<style>
	page{
		background: #BCD2EE;
	}
</style>
