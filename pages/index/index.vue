<template>
	<view class="container">
		<view class="swiper">
			<view class="page-section-spacing">
				<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
					<swiper-item><image class="swiper-img" src="https://www.gymboglobal.com.cn/images/m/course4_pic1.jpg" mode=""></image></swiper-item>
					<swiper-item><image class="swiper-img" src="https://www.gymboglobal.com.cn/files/images/0-5ad0c75b4762c-1523631963.jpg" mode=""></image></swiper-item>
					<swiper-item><image class="swiper-img" src="https://www.gymboglobal.com.cn/files/images/0-5ad0c707a1691-1523631879.jpg" mode=""></image></swiper-item>
				</swiper>
			</view>
		</view>

		<view class="ui-all">
			<view class="ui-list right">
				<text>预约中心</text>
				<picker @change="bindPickerChange" mode="selector" range-key="name" :value="index" :range="address">
					<view class="picker">{{ address[addressIndex].name }}</view>
				</picker>
				<view class="arrow"></view>
			</view>
			<view class="ui-list">
				<text>宝宝姓名</text>
				<input class="list-input" type="text" :placeholder="value" :value="babyName" @input="bindbabyName" placeholder-class="place" />
				<view class="arrow"></view>
			</view>
			<view class="ui-list right">
				<text>宝宝生日</text>
				<picker mode="date" :value="date" @change="bindDateChange" :start="startDate" :end="endDate">
					<view class="picker">{{ date }}</view>
				</picker>
				<view class="arrow"></view>
			</view>
		</view>
		
		<view class="submit-btn" @click="submit">预约免费试听课程</view>
	</view>
</template>

<script>
function getDate(type) {
		const date = new Date();
	
		let year = date.getFullYear();
		let month = date.getMonth() + 1;
		let day = date.getDate();
	
		if (type === 'start') {
			year = year - 15;
		} else if (type === 'end') {
			year = year + 2;
		}
		month = month > 9 ? month : '0' + month;;
		day = day > 9 ? day : '0' + day;
	
		return `${year}-${month}-${day}`;
	}
export default {
	data() {
		return {
			indicatorDots: true,
			autoplay: true,
			interval: 2000,
			duration: 500,
			addressIndex: 0,
			address: [
				{
					id: 1,
					name: '西安曲江星悦荟'
				},
				{
					id: 2,
					name: '西安高新'
				}
			],
			value: '请填写',
			babyName: '',
			date: '请填写',
			startDate:getDate('start'),
			endDate:getDate('end'),
		};
	},
	methods: {
		bindPickerChange(e) {
			this.index = e.detail.value;
		},
		bindbabyName(e) {
			this.babyName = e.detail.value;
		},
		bindDateChange(e) {
			this.date = e.detail.value;
		},
		submit() {
			console.log({
				address: this.address[this.addressIndex].name,
				babyName: this.babyName,
				date: this.date
			})
		}
	}
};
</script>

<style lang="scss">
.container {
}
.swiper,
.swiper-img {
	width: 750upx;
	height: 490upx;
	background-color: #fd8925;
}

.ui-all {
	padding: 20upx 40upx;
	.ui-list {
		width: 100%;
		text-align: left;
		padding: 20upx 0;
		border-bottom: solid 1px #f2f2f2;
		position: relative;

		text {
			color: #4a4a4a;
			font-size: 32upx;
			display: inline-block;
			vertical-align: middle;
			min-width: 150upx;
		}

		input {
			color: #a8a8a8;
			font-size: 30upx;
			display: inline-block;
			vertical-align: middle;
		}
		picker {
			width: 90%;
			color: #808080;
			font-size: 30upx;
			display: inline-block;
			vertical-align: middle;
			position: absolute;
			top: 30upx;
			left: 150upx;
			font-size: 32upx;
		}
		.arrow {
			content: '';
			width: 20upx;
			height: 20upx;
			border-top: solid 1px #a8a8a8;
			border-right: solid 1px #a8a8a8;
			transform: rotate(45deg);
			-ms-transform: rotate(45deg);
			/* IE 9 */
			-moz-transform: rotate(45deg);
			/* Firefox */
			-webkit-transform: rotate(45deg);
			/* Safari 和 Chrome */
			-o-transform: rotate(45deg);
			position: absolute;
			top: 40upx;
			right: 0;
		}
		.list-input {
			color: #030303;
			font-size: 32upx;
			display: inline-block;
			vertical-align: middle;
		}
	}
}
.submit-btn {
	position: fixed;
	bottom: 40upx;
	left: 50%;
	width: 350upx;
	height: 74upx;
	margin-left: -175upx;
	line-height: 74upx;
	color: #fff;
	background-color: #fcbf67;
	text-align: center;
	border-radius: 100upx;
	font-size: 30upx;
}
</style>
