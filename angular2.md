## 1、路由传参
```
<a routerLink="/shop/analysis" [queryParams]="{beginTime: beginTime, endTime: endTime}" ></a>

this.route.queryParams.subscribe((params: Params) => {
      this.beginTime = params['beginTime']
      this.endTime = params['endTime']
    });
    ```
## 2、输入框状态
```
<input type="text" class="form-control" name="shopname" placeholder="序号" [disabled]="addStatus"
                   [(ngModel)]="product.sequence"/>
```                   
