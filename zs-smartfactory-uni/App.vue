<script>
/**
 * Copyright (c) 2013-Now http://aidex.vip All rights reserved.
 */
export default {
	onLaunch() {
		// 国际化，设置当前语言
		if (this.vuex_locale){
			this.$i18n.locale = this.vuex_locale;
			this.$u.api.lang({lang: this.vuex_locale});
		}
		// 设置底部导航栏角标
		uni.setTabBarBadge({
		  index: 1,
		  text: '3'
		});
		// uni.removeTabBarBadge({
		//   index: 0
		// });
	}
}
</script>
<style>
	@import url("~@/static/iconfont/iconfont.css");
</style>
<style lang="scss">
@import "@/static/iconfont.css";
@import "uview-ui/index.scss";
@import "pages/common/aidex.scss";
</style>