{%hackmd SJz188iO_ %}
[![hackmd-github-sync-badge](https://hackmd.io/XeRcOAa-Q966snhT3Dr99w/badge)](https://hackmd.io/XeRcOAa-Q966snhT3Dr99w)

# Angular 產生語法
---
## 常用CLI指令
* ng：指 angular CLI 執行程式
* g：generate 的縮寫，代表『建立』

:::info
* Module
    * ng g module my-module: 產生 Module (模組)程式碼
    * ng g module my-module --routing: 產生 Module (模組)程式碼，含 Routing (路由)
    * ng g guard my-guard: 產生 Guard (路由守門員)程式碼
* Directive
    * ng g component my-new-component: 產生 Component (元件)程式碼 
    * ng g directive my-new-directive: 產生 Directive (指令)程式碼
    * ng g pipe my-new-pipe: 產生 Pipe (管道)程式碼
* Class
    * ng g service my-new-service: 產生 Service (服務)程式碼
    * ng g class my-new-class: 產生 Class 程式碼
* 其他
    * ng g interface my-new-interface: 產生 Interface 介面程式碼
    * ng g enum my-new-enum: 產生 Enum 程式碼
    * ng g app-shell [ --universal-app <universal-app-name>] [ --route <route>]:  建立 App Shell
---
參考文件: https://blog.poychang.net/note-angular-cli/
:::
## Module 模組
:::danger
組成: Module 
裝飾器: @NgModule   
:::
:::info  
    在 /app 底下輸入: ng g m heroes --routing
    /heroes                      (新增)
        heroes.module.ts         (新增)
        heroes-routing.module.ts (新增)
* **.module.ts**:
* **-routing.module.ts**: Router(路由) 
    * 因為多加了 --routing 參數，所以 CLI 多幫我們建立一個路由模組 heroes-routing.module.ts
    *  參考: https://jonny-huang.github.io/angular/training/09_angular_router2/
:::
## Route Guards 路由守衛
:::danger
組成: Class
裝飾器: @Injectable   
:::
:::info 
    在 /app 底下輸入: ng generate guard auth 
    /app 
        auth.guard.ts    (新增)
        auth.guard.spec.ts (新增)
* **.guard.ts**: TypeScript檔
* **.guard.spec.ts**: 單元測試檔
:::
## Component 元件
:::danger
組成: Directive
裝飾器: @Component   
:::
:::info 
    在 /heroes 底下輸入: ng g c ./heroesDetail 
    /heroes-detail (新增)
        heroes-detail.component.html    (新增)
        heroes-detail.component.scss    (新增)
        heroes-detail.component.ts      (新增)
        heroes-detail.component.spec.ts (新增)
* **.component.html**: HTML頁面
* **.component.scss**: CSS檔案
* **.component.ts**: TypeScript檔
* **.component.spec.ts**: 單元測試檔
:::   
## Directive 指令
:::danger
組成: Directive
裝飾器: @Directive  
:::
:::info 
    在 /heroes 底下輸入: ng g directive ./heroes
        heroes.directive.ts           (新增)
        heroes.directive.spec.ts      (新增)
* **.directive.ts**: TypeScript
:::
## Pipe 管道
:::danger
組成: Directive
裝飾器: @Pipe 
:::
:::info 
    在 /heroes 底下輸入: ng g p ./heroes
    /heroes
        heroes.pipe.ts           (新增)
        heroes.pipe.spec.ts      (新增)
* **.pipe.ts**: TypeScript
:::
## Service 服務
:::danger
組成: Class
裝飾器: @Injectable
:::
:::info 
    在 /heroes 底下輸入: ng g s ./heroes
    /heroes
        heroes.service.ts        (新增)
        heroes.service.spec.ts   (新增)
* **.service.ts**: TypeScript
::: 
* Service 則負責像是取得資料、表單驗證等等的邏輯處理
* 來讓我們的應用程式擁有更好的結構與彈性。
* Angular 是怎麼讓 Component 能夠很便利的使用 Service
* 種設計原則叫做 IoC （Inversion of Control，控制反轉），用來減低程式碼之間的耦合度。
* 最常見的方式就是使用 DI(Dependency Injection依賴注入) 。