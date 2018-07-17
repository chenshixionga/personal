### 当文档中存在相关的文件时，仍然报错 :no such file or directory 
 
### 解决方法如下
#### 把.gitbook\versions\3.2.2\lib\output\website\copyPluginAssets.js 里面112行改成confirm：false
