#### 1、安装 less 和 less-loader ，在项目目录下运行如下命令
```
   npm install less less-loader --save-dev
```

#### 2、安装成功后，打开 build/webpack.base.conf.js ，在 module.exports = 的对象的 module.rules 后面添加一段：
```
  module.exports = {

      module: {
          rules: [

            {
              test: /\.less$/,
              loader: "style-loader!css-loader!less-loader",
            }
          ]
      }
  }
```
#### 3、在代码中的 style 标签中 加上 lang="less" 属性即可~
```
  <style scoped lang="less">

  </style>
```

#### 4、在main.js中引入全局less文件
```
  @import './index.less'; //引入全局less文件
```
