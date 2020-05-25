<template>
	<view>
		<table>
			<tr>
				<th>规格名称</th>
				<th>规格项</th>
				<th>价格</th>
				<th>操作</th>
			</tr>
			<tr v-for="(item,index) in specList" :key="index">
				<td>
					<input type="text" v-model="item.name" style="border: 1px solid #000;margin: 10rpx;">
				</td>
				<td>
					<div v-for="(value,valueIndex) in item.valueList" :key="valueIndex">
						<input type="text" v-model="value.name" style="border: 1px solid #000;margin: 10rpx;">
						<input type="text" v-model="value.price" style="border: 1px solid #000;margin: 10rpx;">
						<!-- 删除规格 -->
						<button type="primary" size="mini" @click="delSpecValue(index,valueIndex)">x</button>
						<button type="primary" size="mini" @click="addSpecValue(index)">add</button>
					</div>
				</td>
				<td>
					<button type="primary" size="mini" @click="delSpec(index)">del</button>
				</td>
			</tr>
			<button @click="addSpec">新增规格</button>
			<button @click="submit">提交</button>
		</table>
		<view class="container">
				<div>
					<p v-for="(item,index) in specList">
					{{item.name}}
					<br>
					<span v-for="(value,valueIndex) in item.valueList">{{value.name}}</span>
					</p>
				</div>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				specList:this.specListProp,
				createQuote:[]
			}
		},
		props:{
			data:{
				type:Array,
				default(){
					return []
				}
			},
			specListProp:{
				type:Array,
				default(){
					return []
				}
			}
		},
		watch:{
			specList(){
				this.specList = this.specListProp
			}
		},
		methods: {
			delSpecValue(index,valueIndex){
				if(this.specList[index].valueList.length > 1) {
					this.specList[index].valueList.splice(valueIndex,1)
				}
			},
			addSpecValue(index){
				if(this.specList[index].valueList.length<5) {
					this.specList[index].valueList.push({
						name:'',
						price:''
					})
				}
			},
			delSpec(index){
				this.specList.splice(index,1)
			},
			addSpec(){
				this.specList.push(
					{
						name:'',
						valueList:[
							{name:'',price:''}
						]
					}
				)
			},
			submit(){
				console.log(this.specList)
			}
		}
	}
</script>

<style>

</style>
