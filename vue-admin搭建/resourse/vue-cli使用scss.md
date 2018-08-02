#### 1、安装 node-sass 和 sass-loader ，在项目目录下运行如下命令(sass-loader依赖node-loader)
```
   npm install sass-loader node-sass --save-dev
```

#### 2、安装成功后，打开 build/webpack.base.conf.js ，在 module.exports = 的对象的 module.rules 后面添加一段：
```
  module.exports = {

      module: {
          rules: [
            {
              test: /\.scss$/,
              loaders: ["style", "css", "sass"]
            }
            或者
            {
              test: /\.scss$/,
              use: [
                  "style-loader", // creates style nodes from JS strings
                  "css-loader", // translates CSS into CommonJS
                  "sass-loader" // compiles Sass to CSS, using Node Sass by default
              ]
           }
          ]
      }
  }
```
#### 3、在代码中的 style 标签中 加上 lang="less" 属性即可~
```
  <style scoped lang="scss">

  </style>
```

#### 4、在main.js中引入全局scss文件
```
  @import './index.scss'; //引入全局scss文件
```
