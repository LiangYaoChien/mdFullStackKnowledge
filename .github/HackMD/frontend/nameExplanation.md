{%hackmd SJz188iO_ %}
# 常見名詞
## DevOps
![](https://i.imgur.com/R8MIVbB.png)

* Development(開發)和Operations(運營)的組合詞
* Development 指的是軟體開發
* Operation 主要指的是技術運營＆維護
* 可視為: 軟體開發、技術運維及品質保障 (Quality Assurance, QA) 的交集。
* 參考文件: https://www.cakeresume.com/resources/what-is-devops?locale=zh-TW

![](https://i.imgur.com/kzXuA8R.png)

## MVC
![](https://i.imgur.com/O1GLFxA.png)

## 敏捷開發

## 測試驅動開發(TDD)
* 指的是開發模式
* 可分為四種: TDD、ATDD、BDD、DDD
![](https://i.imgur.com/qHBI1gW.png)
* [詳細說明](https://hackmd.io/LXei80ayQfKem019L7HcpA?view#TDD)
### 測試類型
* 可分為以下幾種:
    * 單元測試
    * 整合測試
    * E2E測試
### 實作順序
* 當使用者向產品經理（需求分析人員）提出需求時: 
    * 若有實作DDD
        * 會先行導入商務端的知識，反映領域內使用者需求的本質。
* 產品經理（需求分析人員）與研發團隊一起梳理用戶故事:
    * 若有實作ATDD
        * 實例化用戶故事驗收條件。
    * 若有實作BDD
        * 就會產出 .feature檔(腳本)
        * 裡面是用人話形容使用者需求。
        * 著重在: 系統的行為，也就是說它應該如何執行。
* 梳理完User Story:
    * 研發人員（測試人員）使用BDD工具，
        * 把 .feature檔(腳本) → 轉成可以運行的驗收測試說明文檔。
        * 轉出來的驗收測試 可能只是外殼，需要研發人員補上method。
            > E2E測試 是 常見的驗收測試之一。
* 研發人員撰寫測試案例、實現代碼:
    1. 撰寫 E2E測試的method 紅燈。
    2. 撰寫 整合測試 紅燈。
    3. 撰寫 單元測試 紅燈。
    4. 實現代碼 讓 單元測試 綠燈。
    5. 實現代碼 讓 整合測試 綠燈。 (此時程式應該已全部完成)
    6. 最後再確認 E2E測試 是否已轉成綠燈。

## CI / CD

## 自動測試

## SOLID原則

## Clean Code

## Interface
* 參考: https://hackmd.io/@ycLiang/H1wddr6v_