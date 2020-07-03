# page-select

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

![](https://github.com/RLflash/page-select/blob/master/theme/1.png)
![](https://github.com/RLflash/page-select/blob/master/theme/2.png)
![](https://github.com/RLflash/page-select/blob/master/theme/3.png)

### 参数

| 参数              | 默认参数 |              | 子参数          |                          | 默认参数 |
| ----------------- | -------- | ------------ | --------------- | ------------------------ | -------- |
| showSelect (必填) |          | 输入框数据   | placeH (可选)   | 输入框placeholder        | ''       |
|                   |          |              | dataKey (必填)  | 输入框所要展示数据的字段 |          |
| seachQuery (可选) | ［］     | 搜索条件数据 | seachKey (继承) | 查询输入框条件字段       |          |
|                   |          |              | placeH (继承)   | 查询输入框placeholder    |          |
| tableHead (可选)  | ［］     | 表单头部数据 |                 |                          |          |
| tableData (可选)  | ［］     | 表单展示数据 |                 |                          |          |
| pageData (可选)   |          |              | total (继承)    | 总数据数量               | 100      |
|                   |          |              | current (继承)  | 当前页                   | 1        |
|                   |          |              | size (继承)     | 每页多少条数据           | 10       |

### 方法

getQuery
返回查询条件，在这里可以进行数据请求

getSelectData
返回选中数据，用于输入框展示

```
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
```

