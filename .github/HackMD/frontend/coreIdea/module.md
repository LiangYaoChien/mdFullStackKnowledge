{%hackmd SJz188iO_ %}
# Module
* Module就像是一個打包好的功能，可視為Components封裝的單位。
* 這個打包好的功能可以給其他的module使用，自身也可以導入其他的Module。
* 可以分享在module中的Component和共享Service給其他Module，
* 可以使用已經定義好的@NgModule。
## 產生語法 
* https://hackmd.io/@9EyeDK2yRQCYuyR8qrqhsw/SygXGCeuO#Module-%E6%A8%A1%E7%B5%84
## 結構
```javascript=
import { NgModule } from '@angular/core';

// 顯示參考 (CodeLens) 指定語言 - 平常註解, 需要在使用
@NgModule({
    declarations: [
        // 宣告: 可控制DOM、跟樣版有關的程式 Component(元件)、Directive(指令)、Pipe(管線)   
        AppComponent, 
        HighlightDirective, 
        PasswordPipe,
    ],
    imports: [
        // 宣告: 『內部』使用的Module(模組) 包含 Routing
        FormsModule,
        WorkprojectRoutingModule,
    ],   
    providers: [
        // 實作: 注入 service(服務)
        WorkprojectService,

        // 攔截器  參考: https://angular.tw/guide/http
        { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
    ],
    exports: [
        // 開放『外部』使用 Module(模組)、Component(元件)、Directive(指令)、Pipe(管線)、service(服務)

    ],        
    entryComponents: [
        // 定義此 NgModule 中要編譯的元件集，這樣它們才可以動態載入到檢視中

    ],
    bootstrap: [
        //根元件: 設定在一開始要進入的『模組成員(元件)』是那一個        
        AppComponent,
    ]


})
export class AppModule { }
```

# RouterModule
## 結構
* 根Routing
```javascript=
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  { path: '', redirectTo: '/heroes', pathMatch: 'full' },
  { path: 'heroes', component: HeroesComponent },  
  { path: 'detail/:aa', component: HeroesDetailComponent },
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class HeroesRoutingModule { }
```
* 子Routing
```javascript=

```
## 延遲載入 vs 預先載入
* 預設是延遲載入Module
* 如果要改成預先載入, 需在app-routing.moudle.ts新增參數: preloadingStrategy: PreloadAllModules
### 模組延遲載入
* 進入該路由的時候才會即時載入Module.js    
* 範例:
    * http://localhost:4200/
        * 未載入t-t-module.js
        ![](https://i.imgur.com/hzEcCKC.png)
    * http://localhost:4200/t
        * 載入t-t-module.js
        ![](https://i.imgur.com/wsr1zfF.png)
> 
* 寫法: 
    * t-routing.module.ts
        ```javascript=
        {
            path: 't',
            loadChildren: () => import('./t/t.module').then(m => m.TModule)
        }
        ```
### 模組預先載入
* 頁面初始化的時候，就把所有可延遲載入的模組，透過背景非同步地下載，不會影響畫面的顯示或使用者的操作。
* 範例:
    * http://localhost:4200/
        * 直接載入t-t-module.js
        ![](https://i.imgur.com/dDckU1y.png)
* 寫法:
    * app-routing.moudle.ts
        ```javascript=
        @NgModule({
          imports: [RouterModule.forRoot(routes,
            {
                //新增此參數, 才可改成預先載入
                preloadingStrategy: PreloadAllModules
            })],
          exports: [RouterModule]
        })
        ```
    * t-routing.module.ts
        ```javascript=
        {
            path: 't',
            loadChildren: () => import('./t/t.module').then(m => m.TModule)
        }
        ```
## 網址組成
* 網址
![](https://i.imgur.com/XtakmQB.png)
## URL傳值 
* 參數傳遞種類:
    * URI Segment: `/:name/:id`      ex: /Sam/2
    * Query String: `?後面的參數`    ex: allowEdit=1&allowMap=8
    * Fragment: `(錨點)#後面的參數`   ex: loading 
* URL: http://localhost:4200/heroes/index/detail3/Sam/2?allowEdit=1&allowMap=8#loading
![](https://i.imgur.com/oANO7hw.png)
## 轉址與傳遞參數 
* 轉址: /detail3
* 傳遞參數 :
    * URI Segment:  `/Sam/2`
    * Query String: `allowEdit=1&allowMap=8`
    * Fragment: `loading` 
* 寫法:
    * 方式一: 在HTML透過繫結的方式 (類似href)
        * heroes-index.component.html
        ```javascript=
        <ul>
            <li><a [routerLink]="['detail']" routerLinkActive="router-link-active">detail</a></li>
            <li><a [routerLink]="['detail2']" routerLinkActive="router-link-active">detail2</a></li>
            <li><a [routerLink]="['detail3', 'Sam', 2]"
                    [queryParams]="{allowEdit: 1, allowMap: 8}"
                    fragment="loading">detail3</a></li>
        </ul>

        <router-outlet></router-outlet>
        ```
    * 方式二: 從typescript設定路由怎麼走     
         * heroes-index.component.html
        ```javascript=
        <button (click)="reLoadPage()">Detail3</button>

        <router-outlet></router-outlet>
        ```
        * heroes-index.component.ts:
        ```javascript=
        constructor(private router: Router, private route: ActivatedRoute) { }

        reLoadPage() {
        this.router.navigate(['detail3', 'Sam', 2]
          , { relativeTo: this.route
            , queryParams: { 'allowEdit': 1, 'allowMap': 8 }
            , fragment: 'Loading' });
        }
        ```  
    * 注意: 無論是選擇方式一or方式二，皆須設定routing
        * 檔案: heroes-routing.module.ts
        ```javascript=
        const routes: Routes = [
        {
            path: '',
            component: HeroesContainerComponent,
            children: [
            {
                path: '',
                redirectTo: 'index',
                pathMatch: 'full'
            },
            {
                path: 'index',
                component: HeroesIndexComponent,
                children: [
                {
                    path: 'detail',
                    component: HeroesDetailComponent,
                },
                {
                    path: 'detail2',
                    component: HeroesDetail2Component,
                },
                {
                    path: 'detail3/:name/:id',
                    component: HeroesDetail3Component,
                }]
            }]
        }];

        @NgModule({
          imports: [RouterModule.forChild(routes)],
          exports: [RouterModule]
        })
        export class HeroesRoutingModule { }
        ```  
## 接參數
* 方式一: 快照 Snapshot
    * heroes-detail.component.ts:
    ```javascript=
    this.user = {
        //URI Segment
        name: this.route.snapshot.params['name'],
        id: this.route.snapshot.params['id']
    }

    //Query String
    this.allowEdit = this.route.snapshot.queryParams['allowEdit'];
    this.allowMap = this.route.snapshot.queryParams['allowMap'];

    //Fragment
    this.tag = this.route.snapshot.fragment;
    ```       
* 方式二: 訂閱 Observable  
    * heroes-detail.component.ts:
    ```javascript=
    //URI Segment
    this.route.params.subscribe((Params) => {
        this.user.name = Params['name'],
        this.user.id = Params['id'];
    });               

    //Query String
    this.route.queryParams.subscribe((queryParams) => {
        this.allowEdit = queryParams['allowEdit'],
        this.allowMap = queryParams['allowMap'];
    });

    //Fragment
    this.route.fragment.subscribe((fragment) => {
          this.tag = fragment;
    });
    ```
    * heroes-detail.component.html
    ```javascript=
    URI Segment:<br>
    name: {{ user.name }} / id: {{ user.id }}
    <br><br>
    Query String:<br>
    allowEdit: {{allowEdit}} / allowMap: {{allowMap}}
    <br><br>
    Fragment錨點:<br>
    tag: {{tag}}
    ```
# 範例
* https://stackblitz.com/edit/angular-ycliang-helloworld

