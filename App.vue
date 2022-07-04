<script>
	// #ifdef APP-PLUS
	var jpushModule = uni.requireNativePlugin("JG-JPush")
	// #endif
	export default {
		onLaunch: function() {
			console.log('App Launch')
			// #ifdef APP-PLUS
			//监听 极光推送连接状态
			jpushModule.initJPushService(); //初始化
			this.getRegistrationID();
			
			uni.$on('connectStatusChange',(connectStatus)=>{ 
			   var connectStr = ''
			   if (connectStatus == true) {
				   connectStr = '已连接'
				   this.getRegistrationID()
			   }else {
				   connectStr = '未连接'
			   }
			   console.log('监听到了连接状态变化 --- ', connectStr) 
			   this.connectStatus = connectStr
			}) 
			
			this.getNotificationEnabled();
			this.watchPush();
			// #endif
		},
		onShow: function() {
			console.log(jpushModule);
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		methods:{
			//监听消息推送事件
			watchPush() {
			  jpushModule.addNotificationListener(result => {
				jpushModule.setBadge(0);
				if(result['notificationEventType'] === 'notificationOpened'){
					const extras = result['extras'];
					if(extras){
						uni.navigateTo({
							url:`/pages/index/description?nftRecording=${extras.nftRecording}&nftOriginator=${extras.nftOriginator}`
						})
					}else{
						const reg = /action\=(\S*);component/i;
						const link = result['android']['deeplink'];
						const jumpLink = link.match(reg)[1];
						if(jumpLink){
							uni.navigateTo({
								url:jumpLink
							})
						}
					}
				}
			  });
			},
			// #ifdef APP-PLUS
			getRegistrationID() { //获取registerID
				jpushModule.getRegistrationID(result=>{
					let registerID = result.registerID
					console.log(registerID,"registerID")
					this.registrationID = registerID
					uni.setStorageSync("registerID",registerID)
				})	
			},
			//getNotificationEnabled 和 noticMsgTool 只是个方法名 可以随便起
			getNotificationEnabled(){ 
				if(uni.getSystemInfoSync().platform == "ios"){
					jpushModule.requestNotificationAuthorization((result)=>{
						let status = result.status
						if (status < 2) {
							this.noticMsgTool()
						}
					})
				}else{
					jpushModule.isNotificationEnabled((result)=>{ //判断android是否打开权限
						if(result.code == 0){//如果为0则表示 未打开通知权限 
							this.noticMsgTool()
						}
					})
				}
			},
			noticMsgTool(){
				if(uni.getSystemInfoSync().platform == "ios"){
					//苹果打开对应的通知栏
					uni.showModal({
						title: '通知权限开启提醒',
						content: '您还没有开启通知权限，无法接受到消息通知，请前往设置！',
						showCancel: false,
						confirmText: '去设置',
						success: function(res) {
							if (res.confirm) {
								var app = plus.ios.invoke('UIApplication', 'sharedApplication');
								var setting = plus.ios.invoke('NSURL', 'URLWithString:', 'app-settings:');
								plus.ios.invoke(app, 'openURL:', setting);
								plus.ios.deleteObject(setting);
								plus.ios.deleteObject(app);
							}
						}
					});
				}else{
					//android打开对应的通知栏
					var main = plus.android.runtimeMainActivity();
					var pkName = main.getPackageName();
					var uid = main.getApplicationInfo().plusGetAttribute("uid");
					uni.showModal({
						title: '通知权限开启提醒',
						content: '您还没有开启通知权限，无法接受到消息通知，请前往设置！',
						showCancel: false,
						confirmText: '去设置',
						success: function(res) {
							if (res.confirm) {
							    var Intent = plus.android.importClass('android.content.Intent');
								var Build = plus.android.importClass("android.os.Build");
								//android 8.0引导  
								if (Build.VERSION.SDK_INT >= 26) {
									var intent = new Intent('android.settings.APP_NOTIFICATION_SETTINGS');
									intent.putExtra('android.provider.extra.APP_PACKAGE', pkName);
								} else if (Build.VERSION.SDK_INT >= 21) { //android 5.0-7.0  
									var intent = new Intent('android.settings.APP_NOTIFICATION_SETTINGS');
								    intent.putExtra("app_package", pkName);
									intent.putExtra("app_uid", uid);
								} else { //(<21)其他--跳转到该应用管理的详情页  
									intent.setAction(Settings.ACTION_APPLICATION_DETAILS_SETTINGS);
									var uri = Uri.fromParts("package", mainActivity.getPackageName(), null);
									intent.setData(uri);
								}
							    // 跳转到该应用的系统通知设置页  
							    main.startActivity(intent);
							}
						}
					});
				}
			}
			// #endif
		}
	}
</script>

<style lang="scss">
	@import "@/uni_modules/uview-ui/index.scss";
	/*每个页面公共css */
	*{
		box-sizing: border-box;
	}
	page{
		background-color: #1D201F;
	}
</style>
