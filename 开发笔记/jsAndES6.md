## 深复制
```
  deepCopy (data) {
    return JSON.parse(JSON.stringify(data));
  }
  
  //三点标识数组或对象的第一层拆散，
  this.realOders.push(...orders)
```
## 对象循环
```
   let value = "WHETHER": {
     0: "否",
     1: "是"
    }
   for (let k in value) {
      let key: any = k
      try {
        key = parseInt(key)
      } catch (e) {
      }
      if (isNaN(key)) {
        key = k
      }
      entrys.push({key: key, value: value[key]});
    }
```
