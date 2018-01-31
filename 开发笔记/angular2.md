## 1、路由传参
<a routerLink="/shop/analysis" [queryParams]="{beginTime: beginTime, endTime: endTime}" ></a>

 {
        path: 'analysis',
        component: AnalysisComponent
      },
      
this.route.queryParams.subscribe((params: Params) => {
      this.beginTime = params['beginTime']
      this.endTime = params['endTime']
    });
