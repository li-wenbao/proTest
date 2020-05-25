<template>
	<view class="main">
		<view @click="openMask">打开弹窗</view>
		<dialog-bar v-model="sendVal" type="danger" title="我是标题" content="我是内容" v-on:cancel="clickCancel()" @danger="clickDanger()"
		 @confirm="clickConfirm()" dangerText="Delete"></dialog-bar>

        <view @click="showPopup">测试tank</view>
		<modal v-show="showCar" width="70%">
			<view>
				撒个塞国后
			</view>
			<!-- <template is="myCarPopup" data="{{carList}}"></template> -->
		</modal>
	</view>


</template>
<script>
	import dialogBar from '@/components/poper/poper'
	import dialogBars from '@/components/poper/popers'
	export default {
		components: {
			'dialog-bar': dialogBar,
			'modal':dialogBars
		},
		data() {
			return {
				sendVal: false,
				showCar: false,
			}
		},
		methods: {

			showPopup() {
				this.showCar = true
			},
			onClose() {
				this.showCar = false
			},

			openMask(index) {
				this.sendVal = true;
			},
			clickCancel() {
				console.log('点击了取消');
			},
			clickDanger() {
				console.log('这里是danger回调')
			},
			clickConfirm() {
				console.log('点击了confirm');
			}
		}
	}
</script>
