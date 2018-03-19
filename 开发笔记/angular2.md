## 1、路由传参
```   
<a routerLink="/shop/analysis" [queryParams]="{beginTime: beginTime, endTime: endTime}" ></a>

 {
   path: 'analysis',
   component: AnalysisComponent
 },
 
this.route.queryParams.subscribe((params: Params) => {
      this.beginTime = params['beginTime']
      this.endTime = params['endTime']
    });
```

## 2、json动态增加属性
```
let json = {"name":"kang","age":12}
    json["salary"]=12340
    console.log(json)
    结果：
    json={
      "name":"kankan",
      "age":12,
      "salary":12340
    }
```
