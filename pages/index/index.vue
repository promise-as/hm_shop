<template>
	<view class="home">
		<swiper indicator-dots circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.url" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item, index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<view class="goods_list">
				<view class="goods_item" v-for="item in goods" :key="item.id">
					<image :src="item.url" mode=""></image>
					<view class="price">
						<text>￥{{item.now_price}}</text>
						<text>￥{{item.original_price}}</text>
					</view>
					<view class="name">{{item.name}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: [
					{
						id: 0,
						url: 'https://img.thea.cn/jingjia/public/202007/hbj/szu-wap/images/c_1.png'
					},
					{
						id: 1,
						url: 'https://img.thea.cn/jingjia/public/202007/hbj/szu-wap/images/c_2.png'
					},
				],
				goods: [
					{
						id: 0,
						name: '三星 Galaxy S20 Ultra',
						original_price: '9999',
						now_price: '9699',
						url: 'https://pic.downk.cc/item/5f2aff3a14195aa59421248a.jpg'
					},
					{
						id: 1,
						name: '华为 HUAWEI P40 Pro+',
						original_price: '11048',
						now_price: '7999',
						url: 'https://pic.downk.cc/item/5f2afe7a14195aa5942101be.jpg'
					},
					{
						id: 2,
						name: 'Apple iPhone 11 Pro Max',
						original_price: '9599',
						now_price: '7099',
						url: 'https://pic.downk.cc/item/5f2afc3a14195aa594208f3c.jpg'
					},
					{
						id: 3,
						name: '小米10 Pro',
						original_price: '5499',
						now_price: '4999',
						url: 'https://pic.downk.cc/item/5f2b010d14195aa5942196d3.jpg'
					},
					{
						id: 4,
						name: '一加 OnePlus 8 Pro 5G旗舰',
						original_price: '5399',
						now_price: '4999',
						url: 'https://pic.downk.cc/item/5f2b028e14195aa594222fc2.jpg'
					}
				],
				navs: [
					{
						icon: 'iconfont icon-supermarket',
						title: '黑马超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-phone',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupianx',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon: 'iconfont icon-video',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
		},
		methods: {
			// 获取轮播图的数据
			async getSwipers(){
				// const res = await this.$myRuquest({
				// 	url: '/api/getlunbo'
				// })
				// this.swipers = res.data.message
			},
			// 获取热门商品列表数据
		 	async getHotGoods(){
				const res = await this.$myRuquest({
					url: ''
				})
				this.goods = res.data.message
			},
			// 导航点击的处理函数
			navItemClick(url){
				// console.log(url)
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 50%;
					margin: 20rpx auto 10rpx;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}
				text{
					font-size: 30rpx;
				}
			}
		}
		.hot_goods{
			background: #eee;
			.tit{
				height: 80rpx;
				line-height: 80rpx;
				color: $shop-color;
				text-align: center;
				letter-spacing: 20rpx;
				background: #fff;
				margin: 8rpx 0;
				border-top: 4px solid #eee;
			}
			.goods_list{
				padding: 0 15rpx;
				display: flex;
				flex-wrap: wrap;
				justify-content: space-between;
				.goods_item{
					background: #fff;
					width: 355rpx;
					margin: 10rpx 0;
					padding: 15rpx;
					box-sizing: border-box;
					image{
						width: 80%;
						height: 260rpx;
						display: block;
						margin: 0 auto;
					}
					.price{
						color: $shop-color;
						font-size: 36rpx;
						margin: 15rpx 0 5rpx;
						text:nth-child(2){
							color: #ccc;
							font-size: 28rpx;
							margin-left: 17rpx;
							text-decoration: line-through;
						}
					}
					.name{
						font-size: 32rpx;
						line-height: 50rpx;
					}
				}
			}
		}
	}
</style>
