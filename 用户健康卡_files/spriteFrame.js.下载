(function ( require ) {
	// require路径配置
	var requireConfig = {
		paths : {
			jquery 			: SERVER_PATH + '/bower_components/jquery/dist/jquery.min',
			vue 			: SERVER_PATH + '/bower_components/vue2/vue.min',
			vueRouter 		: SERVER_PATH + '/bower_components/vue2/vue-router.min',
			iview 			: SERVER_PATH + '/fe_components/iview2/iview.min',
			text 			: SERVER_PATH + '/bower_components/text/text',
			util 			: 'public/util/util',
			MINT 			: SERVER_PATH + '/fe_components/mobile/MINT/index',
			TGUI 			: SERVER_PATH + '/fe_components/mobile/tg-ui/index',
			'emap-h5tag' 	: SERVER_PATH + '/fe_components/mobile/tg-ui/emap-h5tag.min',
			axios 			: SERVER_PATH + '/bower_components/vue2/axios.min',
			'emap-mobile' 	: SERVER_PATH + '/fe_components/mobile/emap-mobile.min',
			BH_MOBILE 		: SERVER_PATH + '/fe_components/mobile/BH_MIXIN_SDK',
			// WEIXIN: 'https://res.wx.qq.com/open/js/jweixin-1.2.0',
			selectRoleIndex : '../../itpub/public/mob/component/selectrole/selectrole',
			home 			: '../../itpub/public/mob/component/home/home',
			nopermission 	: '../../itpub/public/mob/component/nopermission/nopermission',
			spriteUtils 	: '../../itpub/public/mob/js/spriteUtil.js?v=20200928',
			publicVueComponent : '../../itpub/public/mob/component',
			'draggable' 	: SERVER_PATH + "/bower_components/vuedraggable/vuedraggable",
			'sortable' 		: SERVER_PATH + "/bower_components/sortable/1.5.1/Sortable.min",
			// qrcode: SERVER_PATH + '/bower_components/qrcode.js/qrcode.js',
			// bhFillStyle: SERVER_PATH +
			// '/fe_components/mobile/bh_utils_mobile',
			emapMin 		: '../../itpub/public/mob/js/emapMin',
			pagelog 		: SERVER_PATH + '/fe_components/sentry/sentry.min',
			cropper 		: SERVER_PATH + '/bower_components/cropper/cropper.min',
			
		},
		shim : {
			// 'qrcode': {
			// exports: 'QRCode'
			// },
			// 'bhFillStyle': {
			// exports: 'bhFillStyle'
			// },
	        vue: {
	            exports : 'Vue'
	        },
			'emap-mobile' : {
				deps : [ 'jquery' ],
			},
			'emapMin' : {
				deps : [ 'jquery' ],
			},
			'pagelog' : {
				deps : [ 'jquery' ]
			},
			iview : [
				'vue'
			]
		},
		waitSeconds : 0

	};

	/**
	 * appLoadAsync用于控制app页面的加载方式 true: app的所有页面为异步加载，只在使用到时加载 false:
	 * app的所有页面在应用初始化时一次性加载
	 */
	window.appLoadAsync = false;

	// 默认的组件库和公共方法以及公共页面
	var requir_default_arr = [ 'jquery', 
	                           'vue', 
	                           'vueRouter', 
	                           'MINT', 
	                           'TGUI', 
	                           'emap-h5tag', 
	                           'emap-mobile', 
	                           'axios', 
	                           'spriteUtils', 
	                           'draggable', 
	                           'emapMin', 
	                           'pagelog', 
	                           'cropper',
	                           'iview' ];

	// 封装的公共vue组件
	var default_component_arr = [ {
		name : 'auditProcess',
		jsPath : 'publicVueComponent/auditprocess/auditProcess'
	}, {
		name : 'noneDatas',
		jsPath : 'publicVueComponent/nonedatas/nonedatas'
	}, {
		name : 'emapFlowView',
		jsPath : '../../itpub/public/mob/component/emapflowview/emapflowview.js?v=20201028'
	} ];

	/**
	 * 用于保存所有模块的全局对象：
	 * <p> defaultModules：默认的组件库和公共方法以及公共页面
	 * <p> pageModules：当前应用的所有页面模块
	 * <p> defaultComponents：封装的公共vue组件
	 */
	window.REQUIRE_MODULES_ARR = {
		defaultModules : requir_default_arr,
		pageModules : [],
		defaultComponents : default_component_arr
	};

	// 配置require
	require.config( requireConfig );

	// 加载框架所需的库和公共页面
	require( requir_default_arr, function ( $, Vue, VueRouter, mintUI, Tg, emap_h5tag, EMAP_MOBILE, axios, sprite, draggable, emapMin, pagelog, cropper, iview ) {

		// 设置拖拽组件
		Vue.component( 'draggable', draggable );

		// 将各个组件库输出到全局作用域
		window.axios = axios;
		window.Vue = Vue;
		window.VueRouter = VueRouter;
		window.mintUI = mintUI;
		window.Tg = Tg;
		window.emap_h5tag = emap_h5tag;
		window.EMAP_MOBILE = EMAP_MOBILE;
		window.WIS_EMAP_SERV = emapMin;
		window.sprite = sprite;

		$.each( emap_h5tag['default'], function ( i, item ) {
			Vue.component( i, item );
		} );

		$.each( Tg['default'], function ( i, item ) {
			Vue.component( item['name'], item );
		} );

		// vue路由组件
		Vue.use( VueRouter );
		// 饿了么移动端组件mint-ui
		Vue.use( mintUI );
		Vue.use( Tg );
		Vue.use( emap_h5tag );
		// EMAP相关vue组件
		Vue.use( EMAP_MOBILE );
		Vue.use( iview );

		// ids认证
		if ( userId != null && userId != undefined ) {
			// 如果是任务中心过来的请求，将不做角色的选择
			if ( sprite.isTaskCenterRequest () ) {
				sprite.getAuthConfig().then( sprite.initApp );
			} else {
				// 获取角色配置相关参数 --> 获取用户授权功能 --> 初始化应用
				sprite.getSelRoleConfig().then( sprite.getAuthConfig ).then( sprite.initApp );
			}
		}
		// 游客
		else {
			// 初始化应用--游客模式
			sprite.initApp_visitor();
		}

	} );

}( require ));