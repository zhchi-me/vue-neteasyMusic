<template>
	<div class="findsheetlist" :style="{width:listwidth,padding:listpadding}"  @click.stop="showSongSheet(showSongSheetId)">
		<div class="content">
			 <div class="image" :style="{ backgroundImage : 'url('+imagesrc+')',backgroundSize:'cover', backgroundPosition:'center'}"></div>
		</div>
		<div class="title" v-if="showbottomtitle">{{bottomtitle}}</div>
	</div>
</template>

<script>
	import store from '../../store'
	
	export default {
		props: {
			listpadding: {
				type: String,
				default: '0'
			},
			imagesrc: {
				type: String
			},
			showbottomtitle: {
				type: Boolean,
				default: true
			},
			bottomtitle: {
				type: String
			},
			listwidth: {
				type: String
			},
			showSongSheetId: {
				type: Number
			}
		},
		data() {
			return {
				data_list: []
			}
		},
		methods: {
			showSongSheet (id) {
				this.$http.get('https://bird.ioliu.cn/netease/playlist?id=' + id)
		        	.then((res) => {
		        		// console.log(res.data)

		        		store.dispatch({
							type: 'set_MusicSheetList',
							data: res.data
						})
						store.commit({
							type: 'setIsShowSongSheet',
							isShow: true
						})
						
		        	})
		        	.catch(function(error){
		        		console.log(error)
		        	})
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.findsheetlist
		display:inline-block
		width:100%
		box-sizing:border-box
		height:auto
		position:relative
		vertical-align:top
		.content
			width:100%
			height:auto
			position:relative
			.image
				width:100%
				height:0;
				padding-top:100%
		.title
				width: 100%
				height:34px
				line-height:17px
				margin:4px 0
				padding:0 3px
				box-sizing:border-box
				overflow: hidden
				color:#333
				font-weight:400
				text-overflow: ellipsis
				font-size:12px
				display: -webkit-box
				-webkit-line-clamp: 2
				-webkit-box-orient: vertical
</style>