### 1、Excel导出需安装包

npm install -S file-saver

npm install -S xlsx

npm install -D script-loader

### 2、封装过程
 
 ① 拷贝 market-vue项目的vendor文件夹中 Blob.js与Export2Excel.js文件
 
 ② 在使用的地方引入需要文件
 ```
   import { parseTime } from '@/utils'
 ```
 
 ③ 使用已经封装Export2Execl.js，method方法
 ```
  handleDownload() {
      import('@/vendor/Export2Excel').then(excel => {
        const tHeader = ['订单号', '总价格', '供应商', '地址', '状态']
        const filterVal = ['order_name', 'amount_total', 'partner_name', 'receiving_street', 'state']
        const list = this.list
        const data = this.formatJson(filterVal, list)
        excel.export_json_to_excel({
          header: tHeader,
          data,
          filename: this.filename,
          autoWidth: this.autoWidth
        })
      })
    },
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => {
        if (j === 'timestamp') {
          return parseTime(v[j])
        } else {
          return v[j]
        }
      }))
    }
 ```
 
注： [market-vue项目](https://github.com/chenshixionga/market-vue)
 
 
