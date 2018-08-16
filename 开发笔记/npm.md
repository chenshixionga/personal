###### 当使用   npm install   安装失败时：

###### 建议不要使用cnpm install或者update 它的包都是一个link，反正会有各种诡异的bug，这里建议这样使用
```
    npm install --registry=https://registry.npm.taobao.org
```

###### 具体包的安装
```
  npm install echarts --save --registry=https://registry.npm.taobao.org
```

###### 直接设置npm为淘宝镜像
```
    npm config set registry https://registry.npm.taobao.org
```
