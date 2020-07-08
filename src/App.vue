<template>
  <div id="app">
		<el-form ref="form" style="width:460px" label-width="80px">
			<el-form-item label="手机号">
				<page-select 
				v-model="value"
				@getQuery="getQuery" 
				@getSelectData="getSelectData"
				:show-select="showSelect"
				:table-data="tableData" 
				:table-head="tableHead" 
				:seach-query="seachQuery"
				:page-data="pageData"
				>
				</page-select>
			</el-form-item>
		</el-form>
  </div>
</template>
<script>
import pageSelect from 'page-select'
export default {
  name: 'App',
  components: {
    pageSelect
  },
	data(){
		return {
			value:'111',
			showSelect:{'placeH':'请输入手机号','dataKey':'mobilePhone'},
			seachQuery:[
				[{'seachKey':'mobilePhone'},{'placeH':'请输入手机号'}], 
				[{'seachKey':'name'},{'placeH':'请输入姓名'}], 
			],
			tableHead:[{'mobilePhone':'手机号'},{'name':'姓名'}],
			tableData: [{'mobilePhone':11111111111,'name':'张三'},{'mobilePhone':22222222,'name':'李四'}],
			pageData:{'total':100,'current':1,'size':10}
		}
	},
	methods:{
		getQuery(val){
			// 请求数据 val 为请求参数
			console.log(val)
		},
		getSelectData(val){
			this.value=val
		}
	}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
