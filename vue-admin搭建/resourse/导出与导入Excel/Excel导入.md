### 1、安装依赖包 xlsx
```
  　npm install -S xlsx
```

### 2、拷贝 market-vue项目导出组件 UploadExcel 组件

### 3、使用组件
```
   <upload-excel-component :on-success='handleSuccess' :before-upload="beforeUpload"></upload-excel-component>
   
    beforeUpload(file) { // 上传前调用
      const isLt1M = file.size / 1024 / 1024 < 1

      if (isLt1M) {
        return true
      }

      this.$message({
        message: 'Please do not upload files larger than 1m in size.',
        type: 'warning'
      })
      return false
    },
    
    handleSuccess({ results, header }) { // excel文件转为json数据后 调用
      this.tableData = results
      this.tableHeader = header
    }
  
```
