<template>
	<div class="header">
		<div class="header-warpper">
			<i class="menu icon-menu" @click="showMenu"></i>
			<div class="centermenu" @click="hideMenu">
				<router-link tag="i" to="/mymusic">
					<i class="music icon-music"></i>
				</router-link>
				<router-link tag="i" to="/findmusic">
					<i class="find icon-wangyi"></i>
				</router-link>
				<router-link tag="i" to="/community">
					<i class="community icon-community"></i>
				</router-link>
			</div>
			<i class="search icon-search"></i>
		</div>
		<!-- <router-view></router-view> -->
		<keep-alive>
		    <router-view v-if="$route.meta.keepAlive"></router-view>
		</keep-alive>
		<router-view v-if="!$route.meta.keepAlive"></router-view>
	</div>
</template>

<script>
	import store from '../../store'

	export default{
		props: {
			index: {
				type: Number,
				default: 0
			}
		},
		data () {
			return {

			}
		},
		methods: {
			showMenu () {
				console.log('showMenu')
				store.dispatch({
					type: 'showSideBar'
				})
			},
			hideMenu () {
				store.dispatch({
					type: 'hideSideBar'
				})
			}
		}
	}
</script>


<style lang="stylus" rel="stylesheet/stylus">
	.header
		position:fixed
		top:0
		left:0
		right:0
		height:50px
		z-index:10
		background:#C62F2F
		.header-warpper
			height:100%
			background:$primarycolor
			display:flex
			align-items:center
			justify-content:space-between
			.icon-menu,.icon-search
				color:#fff
				font-size:26px
				padding:10px 15px
			.centermenu
				font-size:24px
				i
					margin:0 5px
					color:rgba(255,255,255,0.3)
					&.router-link-active
						i
							color:#fff
</style>