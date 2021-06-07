{%hackmd SJz188iO_ %}
# Angular
| 比較項目 | 前端 | 後端 |
|--:|:--:|:--:|
|語言|[Angular][-NG]</br> with ( [TypeScript][-TS] & [RxJs][-RX] )|C#|
|底層|[NodeJs][-ND]|.Net framework|
|開發工具|[Visual Studio Code][-VSC]|Visual Studio 2015 / 2017|
|套件管理工具|[NPM (Node Package Manager)](https://www.npmjs.com/)|NuGet|
|套件設定檔|package.json|packages.config|
|版本管控|Git（GitFlow）|Git（GitFlow）|
* Angular 應用是模組化的，它擁有自己的模組化系統，稱作 NgModule。
* NgModule: Angular基本構成要素。
    * 一個NgModule 就是一個容器。
    * 功用: 為元件提供了編譯的上下文環境。
    * 用於存放一些內聚的程式碼塊，這些程式碼塊專注於某個應用領域、某個工作流或一組緊密相關的功能。 
    * 它可以包含一些元件、服務提供者或其它程式碼檔案，其作用域由包含它們的 NgModule 定義。
    * 它還可以匯入一些由其它模組中匯出的功能，並匯出一些指定的功能供其它 NgModule 使用。
* Angular 特性
    * [SPA](https://hackmd.io/FxjZTfJURQemM6knCLBa7A?view#%E5%96%AE%E4%B8%80%E7%B6%B2%E9%A0%81SPA%E4%B8%8D%E6%8F%9B%E9%A0%81)
    * Tree Shaking
        * 在Build的時候，會把定義好的代碼、但又沒用到的代碼去掉，不把這些沒用的代碼，打包到最後的bundle文件裡。
        * 優點
            1. 可以減小bundle的體積。
            2. 提高應用性能。
## Typescript
### [符號解釋](/@ycLiang/B15m0dUDO)
## CLI語法
* `ng new helloWorld` : 新增Angular專案
* `npm install`
* `npm start`: 本機執行
    * `ctrl + c`: 停止本機執行
### 新增Angular專案
* 語法: ng new helloWorld
* 會遇到的問句:
    * Do you want to enforce stricter type checking and stricter bundle budgets in the workspace?
  This setting helps improve maintainability and catch bugs ahead of time.
  For more information, see https://angular.io/strict (Y/N)
        * 意为是否要使用更严格的数据类型检查，输入Y即可
    * Would you like to add Angular routing? (Y/N)
        * 意为是否增加路由，输入Y即可
    * Which stylesheet format would you like to use? (Use arrow keys)
      > CSS
      SCSS   [ https://sass-lang.com/documentation/syntax#scss                ]
      Sass   [ https://sass-lang.com/documentation/syntax#the-indented-syntax ]
      Less   [ http://lesscss.org                                             ]
      Stylus [ https://stylus-lang.com                                        ]
        * 你要用哪种CSS样式，随便选一个用的熟练的就行。
## 檔案介紹
![](https://i.imgur.com/LXRsOOX.png)
### /e2e
*  E2E 測試 （End-to-End Testing） 的程式碼要擺放的位置。E2E 測試是使用程式來模擬
      實際使用者的操作來進行的一種測試方式。Angular 在 E2E 測試方面是使用自己特製的工具 
      Protractor。Angular CLI 在建立專案時也會連帶建立範例。

---
### /node_modules
*  Angular自帶函式庫
*  npm實際安裝『確定版本』 的東西

---
### /src 
:::danger
主要在開發的所有程式碼都會放在這裡
::: 
*  /app
    #### 前端的所有專案都是放在這裡
    ![](https://i.imgur.com/A1ELFsz.png)
    * 整個網頁應用程式的 Module、Component、Service、pipe 等等都放在這。
    * 除了 E2E 測試的程式碼之外，大概有九成九都是放這裡

    :::danger
    index.html 讀取Tag <app-root> 
    ![](https://i.imgur.com/4xycoTZ.png)
    → app.component.ts 
    ![](https://i.imgur.com/Iy67R30.png)
    ▲ 注意: templateURL、template: 只能二選一
     ```javascript=
     // 原先: 讀取html頁面
     // templateURL: './app.component.html'      
     // 可改成: 直接寫死HTML語法
     template: `<router-outlet></router-outlet>`
     ```     
     → <router-outlet></router-outlet> 該區塊會透過Routing的方式，輸入不同的網址，就會顯示不同的Component
    → app-routing.module.ts
    → 可直接指定到 某一個Component、或是 某一個Module
    ![](https://i.imgur.com/Dk7cJDQ.png)
    參考: https://angular.tw/api/router/RouterModule    
    :::    
*  /assets
    *  靜態資源放置處，如圖片。
*  /environments
    * 環境變數設定檔放置處
    ![](https://i.imgur.com/CF7HTRE.png)
    * 本機建置: ng s  => 讀取environment.ts
    * ng build => 讀取environment.ts
    * ng build --prod => 讀取environment.prod.ts    
:::success 
新增環境設定檔
* Config配置 → Configuration組態 → Environment環境參數
* 1. 新增環境變數檔(環境參數)
   ![](https://i.imgur.com/RvIWOQb.png)      
* 2. angular.json(配置+組態) 新增設定屬性(透過 fileReplacements 屬性可以定義環境變數檔案的替換)
    * 組態是配置的一部分
   ![](https://i.imgur.com/VmD437O.png)
    如此一來就可以透過以下指令 來建構(Build)預備環境的應用程式封裝檔
        (1) ng build --prod --configuration=production => 讀取environment.prod.ts
        (2) ng build --prod --configuration=edu => 讀取environment.edu.ts    
參考: https://ithelp.ithome.com.tw/articles/10253530
:::    
:::warning
若要進一步也在 ng serve 中使用此設定，就需要在 angular.json 中的 serve 屬性加入定義。
![](https://i.imgur.com/NpO373N.png)

    如此一來就可以透過以下指令 來Build & Run
    ng serve --configuration=production  => 讀取environment.prod.ts
    ng serve --configuration=edu  => 讀取environment.edu.ts
:::
*  favicon.ico
    *  瀏覽器的網址列、書籤、頁籤上都會用到的小 icon 圖檔

*  index.html
    *  整個網頁應用程式的首頁與根頁面，也是 SPA 唯一的那一頁。

*  main.ts
    *  Angular CLI 在編譯與打包的時候，把這支檔案裡的程式，當做整個網頁應用程式的主要程式進入點。
    ![](https://i.imgur.com/875qP0j.png)
    * 一般也是不會去動到這裡的程式碼。
    
*  polyfills.ts
    *  這個檔案滿重要的。
    *  主要是在載入 Angular 的程式之前，會預先載入的程式。
    *  裡面也有一些是如果需要支援較低版本的瀏覽器時，需要取消註解的程式。

    ![](https://i.imgur.com/aTIfO7f.png)

*  styles.scss
    *  整個網頁應用程式共用的樣式設定檔
    * 全域 css 樣式
        * CLI 提供語法糖： ~，代表 node_modules 資料夾，例如：
        ```javascripts=
        // 實際路徑 node_modules/bootstrap/dist/css/bootstrap.min.css
        @import   "~bootstrap/dist/css/bootstrap.min.css";
        ```

*  test.ts
    *   跟 main.ts 檔類似，不過主要是用在測試檔上。
---
### .browserslistrc
* Angular 的編譯器會根據此檔案的設定來加上 CSS 的前綴。
* 用途: 
    * CLI 會使用 Autoprefixer 來確保對不同瀏覽器及其版本的相容性，若你要從建構中針對特定的目標瀏覽器或排除指定的瀏覽器版本時，則需要針對此檔案做調整。
* 運作方式:
    * 內部 Autoprefixer，會依照名叫 Browserslist 的函式庫，來指出需要為哪些瀏覽器加字首。
    * 有以下兩中方式可以設定 
* 1. 在 package.json 新增 browserslist 屬性：
```javascript=
"browserslist": [
  "> 0.5%",
  "last 2 versions"
]
```
* 2. 也可以在專案目錄下新增一個新檔案 .browserslistrc，用於指定你要支援哪些瀏覽器
```javascript=
### Supported Browsers
> 0.5%
last 2 versions

``` 
![](https://i.imgur.com/U4idJJf.png)

* 以上參考: https://angular.tw/guide/build
---
### .editorconfig
* 程式碼排版設定檔，用來統一所有程式排版風格。
* 這個檔案可以幫助開發人員在不同的編輯器和 IDE 之間更容易定義與維護一致的編碼樣式
    
---
### .gitignore
* 版本控制用的忽略設定檔。值得一提的是，就算在建立專案時加入 --skip-git 參數，此檔案也會被創建出來。

---
### angular.json
* 版本控制用的忽略設定檔。值得一提的是，就算在建立專案時加入 --skip-git 參數，此檔案也會被創建出來。

---
### karma.conf.js
* Unit Test 設定檔
* 版本控制用的忽略設定檔。值得一提的是，就算在建立專案時加入 --skip-git 參數，此檔案也會被創建出來。
---
### package-lock.json
* 『當前』實際安裝的套件的版本號與來源。
* version: 版本號
* resolved: 套件的位置
* integrity: 效驗套件的字串(token)
* 參考來源: https://www.zhihu.com/question/62331583

---
### package.json
* scripts: 定義npm指令 
![](https://i.imgur.com/g8r3S6r.png)
* devDependencies、dependencies: 紀錄套件(軟體包)的確切版本
    * devDependencies 裡面的插件只用於開發環境 
        * 構建工具比如glup、webpack這些只是在開發中使用的
    * dependencies 是需要發佈到生產環境
        * 比如我們寫一個項目要依賴jQuery，沒有這個包的依賴運行就會報錯，這時候就把這個依賴寫入dependencies，會被打包進最終的js文件裡。

:::info
* npm install 安裝的時候，有兩種命令把他們寫入到package.json 文件裡面去
    1。 --save-dev：被寫入到devDependencies  
    2。 --save：被寫入到dependencies

:::
:::danger
* 如果改了package.json，且package.json和lock文件不同，那么执行`npm i`时npm会根据package中的版本号以及语义含义去下载最新的包，并更新至lock。
* 如果两者是同一状态，那么执行`npm i `都会根据lock下载，不会理会package实际包的版本是否有新。
:::

---
### README.md
* 這個檔案是這個專案的說明文件，採用 Markdown 的語法。可以自由撰寫關於此專案的任何說明。

---
### tsconfig.app.json
* 跟外層的 tsconfig.app.json 用途類似，在這個檔案裡也會看到有繼承外層的 tsconfig.app.json 的設定

---
### tsconfig.json
* TypeScript 編譯時看的編譯設定檔。
* 參考: https://yiyingloveart.blogspot.com/2016/07/typescript-tsconfigjson.html

---
### tsconfig.spec.json
* 跟 tsconfig.app.json 用途類似，不過主要是針對測試檔。

---
### tslint.json
* 這個檔案是 tslint 套件設定檔。
* TSLint 是 TypeScript 的格式驗證工具，它可以檢查你寫出來的 TypeScript 的格式是不是具有可讀性、可維護性和功能性錯誤。
* 目前改用 ESLint  (讀.eslintrc.json)
# 建立開發環境
## 工具下載與安裝
+ 下載 開發環境 [NodeJs](https://nodejs.org/en/)
      - 請選擇穩定版（**LTS**）
      - 確認你的 NodeJs 是 8.9.1 以上 [(參考 - NodeJs 與 npm 版本對應)](https://nodejs.org/en/download/releases/)
+ 下載 開發工具 [Visual Studio Code](https://code.visualstudio.com/)
      - 如果開發環境有 prxoy，在 NodeJs 與 Visual Studio Code 安裝完後，先看 ==**Proxy 設定**==
+ 必裝 [Angular CLI](https://github.com/angular/angular-cli) 命令列工具：
    - 開啟 Command Line 輸入 ==**npm install -g @angular/cli**==，按下 Enter
   - ![](https://i.imgur.com/Jk7vaGz.png)
   - 當套件有重大改版時，請『依序』使用下列指令進行移除與重新安裝
     1. **`npm uninstall -g @angular/cli`**
     2. **`npm cache verify`**
     3. **`npm install -g @angular/cli`**
+ 必裝 Visual Studio Code 套件：
     - [Angular Extension Pack](https://marketplace.visualstudio.com/items?itemName=doggy8088.angular-extension-pack)：Angular 整合套件包
        ![](https://i.imgur.com/cD88r7O.png)
                安裝後請做下列設定 
          (1) File => Preferences => Setting
          (2) 改為 json 顯示
          (3) 把下列的設定貼到右方的 `USER SETTINGS`

```javascript=
{
    // "editor.snippetSuggestions": "top", // 提高 code snippet 建議順序-有疑問
    "html.format.wrapLineLength": 0,
    "html.format.wrapAttributes": "force-aligned", // HTML 屬性強制換行
    "auto-rename-tag.activationOnLanguage": ["html", "xml"],
    "editor.fontLigatures": true,
    "editor.fontFamily": "Fira Code, Consolas, 'Courier New', monospace",
    "editor.minimap.renderCharacters": false,
    "emmet.showSuggestionsAsSnippets": true,
    "typescript.updateImportsOnFileMove.enabled": "never",
    "window.titleBarStyle": "custom", // 拿掉 vscode 最上面的 bar (建議)
    "editor.codeActionsOnSave": {
      "source.organizeImports": true  // 自動整理 import，並移除沒使用的import
    },
    "editor.formatOnSave": true,      // 存檔自動排版
}
```


* 補充
```javascript=
{
    // 顯示參考 (CodeLens) 指定語言 - 平常註解, 需要在使用
    "javascript.referencesCodeLens.enabled": true,     
    "typescript.implementationsCodeLens.enabled": true,
    "typescript.referencesCodeLens.enabled": true,
}
```

+ 選裝 Visual Studio Code 套件：
    - [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer)：很多顏色的 ==**{ }**==，增加程式可讀性
    - [VsCode Icons](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)：檔案前加上圖示
    - [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)：Typescript 逐步偵錯 
    - [Quokka.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode)：適合練習或驗證 RxJs 功能

### 第三方套件 (Next 預設安裝套件)
1. 樣版套件 - [Bootstrap v4.x](https://bootstrap.hexschool.com/docs/4.1/getting-started/introduction/)
    * 純 CSS 部分可以直接套用
    * 需要額外引用 **JavaScript** 的部分，採用第三方套件 [ngx-Bootstrap][-ngxBootstrap]
      * [ngx-bootstrap][-ngxBootstrap]：把 bootstrap 內的 JavaScript 包成為 Angular Module
3. 圖示套件 - [Font Awesome v4.7][-FontAwesome]
   * 多種 Icon 可以使用
   * 有基本動畫功能
   * Icon 可以重疊組合成新的 Icon
   * 詳細的操作方式請[點我](https://fontawesome.com/v4.7.0/examples/)
4. 圖表套件 - [ECharts](http://echarts.baidu.com/examples/)
   * IE 支援度佳
   * 範例樣式多
   * **商業使用免授權**
   * 補充 - 曾經考慮過的圖表套件
      * highCharts：商業使用需要授權
      * D3Js：學習時間長
      * [ngx-charts][-NGXC]：要求 IE-11 以上，部分功能不相容 IE


[-NG]:https://angular.io/
[-CLI]:https://github.com/angular/angular-cli
[-ND]:https://nodejs.org/
[-VSC]:https://code.visualstudio.com/
[-TS]:https://www.typescriptlang.org/
[-RX]:http://reactivex.io/rxjs/

[-ngxBootstrap]:https://valor-software.com/ngx-bootstrap/#/getting-started
[-FontAwesome]:https://fontawesome.com/v4.7.0/icons/
[-NGXC]:https://swimlane.github.io/ngx-charts/#/ngx-charts/bar-vertical