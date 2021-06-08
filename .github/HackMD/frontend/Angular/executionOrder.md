{%hackmd SJz188iO_ %}
# 執行順序
---
## Angular 執行方式
* Agular 整個網頁應用程式進入點(/src/main.ts)
* 步驟一: 讀取根模組
    > 根模組: 每一個專案都一定會有一個根模組，也就是root module。
    * 我們會在/src/main.ts去做bootstrapModule這個根模組的動作，讓整個APP可以運行起來。
    * /src/main.ts
        ```javascripts=
        import { enableProdMode } from '@angular/core';
        import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

        import { AppModule } from './app/app.module';
        import { environment } from './environments/environment';

        if (environment.production) {
          enableProdMode();
        }

        //讀取根模組
        platformBrowserDynamic().bootstrapModule(AppModule)
          .catch(err => console.error(err));

        ```
        > bootstrapModule執行動作:
        > 參考: https://ithelp.ithome.com.tw/articles/10195338
        > 
            1. 會建立好執行環境。
            2. 並把在src/app/app.module.ts裡設定的bootstrap陣列裡的『根元素』取出來。
            3. 並透過在該成員裡設定的selector，讓我們可以在/src/index.html來顯示這個元件的VIEW。
* 步驟二: 讀取根元件
    * /src/app/app.module.ts
        ```javascript=
        import { NgModule } from '@angular/core';
        import { BrowserModule } from '@angular/platform-browser';
        import { AppRoutingModule } from './app-routing.module';
        import { AppComponent } from './app.component';


        @NgModule({
          declarations: [
            AppComponent
          ],
          imports: [
            BrowserModule,
            AppRoutingModule
          ],
          providers: [],
          bootstrap: [AppComponent]    //讀取根元件
        })
        export class AppModule { }
        ```
* 步驟三: 設定根元件的selector
  * 透過在該成員裡設定的selector，讓我們可以在/src/index.html，顯示這個元件的VIEW。  
  * /src/app/app.component.ts
    ```javascript=
    import { Component } from '@angular/core';

    @Component({
      selector: 'app-root',    //供html叫用
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.scss']
    })
    export class AppComponent {
      title = 'helloWorld';
    }

    ```
* 步驟四: 顯示VIEW(顯示在Index.html上)
    * /src/index.html
    ![](https://i.imgur.com/MdymjwQ.png) 
    
## Angular 關係圖
* -routing.module和Module一起看
![](https://i.imgur.com/ceat7QC.png)
![](https://i.imgur.com/nxouiCJ.png)
* angular打包時，運作邏輯
    * Angular CLI 在編譯與打包的時候，把(main.ts)這支檔案裡的程式，當做整個網頁應用程式的主要程式進入點 
![](https://i.imgur.com/Lpmf5iC.png)
* RouterModule 
    ![](https://i.imgur.com/VI1J8nZ.png)
