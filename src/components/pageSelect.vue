<template>
	<div class="page-select-wrap">
		<el-input ref="input" v-model="tempValue" class="input" :placeholder="showSelect.placeH" @click.native="showTable"/>
		<div class="page-table-wrap" v-if="tableShow">
			<div class="page-tabel-head">
				<el-input v-for="(item,index) in seachQuery" 
				v-model="listQuery[item[0].seachKey]" 
				:key="index" 
				:placeholder="item[1].placeH" style="width: 200px;" class="filter-item"/>
				<el-button class="filter-item" type="primary" icon="el-icon-search" @click="seach">
					搜索
				</el-button>
				<i class="close el-icon-close" @click="close"></i>
			</div>
			<template>
				<el-table :data="tableData" style="max-height: 500px;max-width:100%;overflow:auto" @current-change="handleCurrentChange">
					<el-table-column v-for="(headStr,index) in tableHead" 
					:key="index" 
					:label="headStr[Object.keys(headStr)[0]]" 
					:prop="Object.keys(headStr)[0]">
					</el-table-column>
				</el-table>
			</template>
			<el-pagination
				background
				@size-change="handleSizeChange"
				@current-change="pageCurrentChange"
				layout="total, sizes, prev, pager, next, jumper"
				:current-page=listQuery.current
				:page-size=listQuery.size
				:total=listQuery.total
				class="page-tabel-pagination">
			</el-pagination>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'pageSelect',
		props: {
			tableData:{
				type:Array,
				default(){
					return [];
				}
			},
			tableHead:{
				type:Array,
				default(){
					return [];
				}
			},
			seachQuery:{
				type:Array,
				default(){
					return [];
				}
			},
			showSelect:{
				type:Object,
				default(){
					return {'placeH':''};
				}
			},
			pageData:{
				type:Object,
				default(){
					return {'total':100,'current':1,'size':10}
				}
			},
			value:{
				type:[Number,String],
				default: undefined
			},
		},
	
		data() {
			return {
				list: null,
				selectVal:undefined,
				tempValue:this.value,
				total: 1,
				listData: {
					id: undefined,
				},
				tableShow: false,
				listLoading: true,
				listQuery: {

				}
			}
		},
		watch: {
			tempValue: function(newVal){
				this.$emit('getSelectData',newVal)
			}
		},

		created() {
			Object.assign(this.listQuery,this.pageData)
		},
		methods: {
			getList() {
				this.listLoading = true
			},
			close() {
				this.tableShow = false
			},
			showTable(){
				this.tableShow=true
			},
			seach() {
				this.$emit('getQuery',this.listQuery)
			},
			handleCurrentChange(val) {
				this.tempValue=val[this.showSelect.dataKey]
				this.tableShow = false
			},
			handleSizeChange(val) {
				this.listQuery.size=val
				this.$emit('getQuery',this.listQuery)
			},
			pageCurrentChange(val) {
				this.listQuery.current=val
				this.$emit('getQuery',this.listQuery)
			}
		}
	}
</script>
<style scoped>
	.page-table-wrap {
		width: 1000px;
		padding: 10px;
		margin-top: 10px;
		position: absolute;
		background: #fff;
		z-index: 1;
		box-shadow: 0 0 10px #efebeb;
		border-radius: 10px;
	}

	.page-tabel-head {
		text-align: left
	}
	.page-tabel-pagination{margin-top:20px}
	.el-button {
		margin-left: 10px
	}


	.edit-input {
		padding-right: 100px;
	}

	.cancel-btn {
		position: absolute;
		right: 15px;
		top: 10px;
	}

	.el-input {
		margin: 10px 10px 0 0
	}

	.el-input:first-child {
		margin-left: 0
	}

	.close {
		position: absolute;
		right: 15px;
		top: 13px;
		cursor: pointer;
		z-index: 1000;
		font-size: 25px;
	}
</style>
