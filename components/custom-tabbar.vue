<template>
  <u-tabbar
			:value="value6"
			@change="name => value6 = name"
			:fixed="true"
			:placeholder="true"
			:safeAreaInsetBottom="true"
			activeColor="#333333"
			inactiveColor="#333333"
		>
			<u-tabbar-item text="首页">
				<image
					class="u-page__item__slot-icon"
					slot="active-icon"
					src="../static/home-d.png"
				></image>
				<image
					class="u-page__item__slot-icon"
					slot="inactive-icon"
					src="../static/home.png"
				></image>
			</u-tabbar-item>
			<u-tabbar-item text="元宇宙">
				<image
					class="u-page__item__slot-icon"
					slot="active-icon"
					src="../static/meta-d.png"
				></image>
				<image
					class="u-page__item__slot-icon"
					slot="inactive-icon"
					src="../static/meta.png"
				></image>
			</u-tabbar-item>
			<u-tabbar-item text="我的">
				<image
					class="u-page__item__slot-icon"
					slot="active-icon"
					src="../static/user-d.png"
				></image>
				<image
					class="u-page__item__slot-icon"
					slot="inactive-icon"
					src="../static/user.png"
				></image>
			</u-tabbar-item>
		</u-tabbar>
</template>

<script>
export default {
    name: 'CustomTabbar',
    data(){
        return{
            value6: 0
        }
    }
}
</script>

<style lang="scss" scoped>
.u-page {
		padding: 0;
		&__item {
			&__title {
				color: $u-tips-color;
				background-color: $u-bg-color;
				padding: 15px;
				font-size: 15px;
				&__slot-title {
					color: $u-primary;
					font-size: 14px;
				}
			}
			&__slot-icon {
				width: 17px;
				height: 17px;
			}
		}
	}
</style>