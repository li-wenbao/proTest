<template>
	<view class="page">
		<view class="width100 bg-white">
			<view class="padding-sm margin-top">
				<view class="text-gray">
					规格项
				</view>
			</view>
			<view class="padding-sm" v-for="(item,index) in specList" :key="index">
				<view>
					<view class="flex justify-between margin-top">
						<view class="text-gray">
							{{item.name}}
						</view>
						<view>
							<text class="bg-blue padding-xs shadow"  @click="addSpecValue">+</text>
							<text class="bg-blue padding-xs margin-left-xs" @click="delSpec(index)">-</text>
						</view>
					</view>
					<view class="" v-for="(value,valueIndex) in item.valueList" :key="valueIndex">
						<view class="cu-btn line-gray margin-sm padding-sm">
							<view>
								<text>{{value.name}}</text><text class="margin-left-sm">{{value.price}}元</text>
							</view>
							<text class="bg-blue margin-left-xs" @click="delSpecValue(index,valueIndex)">x</text>
						</view>
					</view>
				</view>
			</view>
			<view class="flex justify-center align-center">
				<text class="bg-blue padding-xs margin-xl" @click="addSpec">+</text>
			</view>
		</view>
	</view>
</template>

<script>
	import {
		data
	} from './index.js'
	import TheProblem from '@/components/MM'
	export default {
		data() {
			return {
				data: []
			}
		},
		components: {
			TheProblem
		},
		computed: {
			specList() {
				let result = []
				data.forEach(item => {
					item.propertyList.forEach(property => {
						// 查找 result 是否有 property.name 这一项, 返回一个布尔值
						let target = result.find(spec => {
							return spec.name === property.name
						});
						/*	
							target:
								true
								false
						*/
						if (!target) {
							result.push({
								name: property.name,
								valueList: [{
									name: property.value,
									price: property.price
								}]
							})
						} else {
							if (!target.valueList.find(value => value.name === property.value)) {
								target.valueList.push({
									name: property.value,
									price: property.price
								})
							}
						}

					})
				});
				return result
			}
		},
		mounted() {
			setTimeout(() => {
				this.data = data
			}, 500)
		},
		methods: {

		}
	}
</script>

<style>
	page {
		background: #333333;
	}

	.header {
		position: relative;
		z-index: 1
	}

	.bgImage {
		background-size: 100% 100%;
		position: relative;
	}

	.mask {
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		background: rgba(12, 12, 12, 0.4);
	}
</style>
