# 簡介
此為大學畢業專題，
本專題透過設計並建立持續整合(CI)與持續部署(CD)的Pipeline，
完成自動化部署，來達成DevOps的概念。
# 專題架構
![](https://hackmd.io/_uploads/rknCfml-T.png)

# 實作方法與使用工具
### 使用工具

* Mocha Framework: 
提供Javascript單元測試的框架
能在Node.js和瀏覽器環境運行
* GitLab:
提供版本控制與CI/CD piepeline
此專題將GitLab做為project repository
* Jenkins: 
知名且市占率高的CI/CD工具
支援許多擴充外掛功能給使用者自行安裝
* Docker: 
透過將應用程式容器化
方便應用程式在不同環境之間快速部署

### 實作方法
使用 Mocha 框架來進行程式前端Javascript的單元測試。

在撰寫完 Dockerfile作為建立Docker Image的腳本後，
將專案、專案所需環境、單元測試與 Dockerfile 
一起透過 Git push 至 GitLab 上。

於 Jenkins 內建立專案並安裝 Docker plug-in，
在專案組態中將程式來源設定為GitLab。

設定專案自動輪詢排程，
使 Jenkins 能夠於固定時間檢查程式來源端-GitLab是否有更新，
以進行自動建置。

撰寫 Docker 指令於Jenkins專案內自動建置的 shell，
使專案建置時能根據 Dockerfile 內容建立 Docker Image，
執行成 Docker Container 以達成部署。

# 實作流程
### 專案建立
Git push project到Gitlab
![](https://hackmd.io/_uploads/HJyz4NxWT.png)

於 Jenkins 中建立Free-Style軟體專案
![](https://hackmd.io/_uploads/rySY7Vl-6.png)

### 在Jenkins安裝Docker plug-in
進入管理Jenkins>>管理外掛程式
![](https://hackmd.io/_uploads/r1oY_ElWa.png)

安裝下方Docker相關插件
![](https://hackmd.io/_uploads/SJbrtNxWT.png)

### 連結GitLab
Jenkins專案連結GitLab做為程式的repository
![](https://hackmd.io/_uploads/rJa9KVgWT.png)

輸入GitLab的Username and Password進行GitLab身分驗證
![](https://hackmd.io/_uploads/r1wl54xZT.png)


### 設定Trigger程序
於建置觸發程序中選擇輪詢SCM
排程可自行設定使Jenkins自動檢查GitLab端的程式專案是否有更新
若有，Jenkins將自動建置專案到最新版本
![](https://hackmd.io/_uploads/ryPLqEg-a.png)

### 設定建置步驟
於建置環境中新增建置步驟
並選擇執行Shell
![](https://hackmd.io/_uploads/r1Ph94l-T.png)

在建置的Shell中輸入docker指令
即可在建置時Build Docker Image
![](https://hackmd.io/_uploads/ByaNs4lbp.png)

### 建置完成
建置完成後於 Image 清單中可見建立完成的 Docker Image
![](https://hackmd.io/_uploads/H1G2iElWT.png)

Container執行完即完成部署
![](https://hackmd.io/_uploads/Bycr34lW6.png)


# 成果
運用 GitLab、Jenkins、Docker 設計好一個自動化部署流程，
並使用碩班學長寫好的專案(使用環境:nodejs、react)，
通過單元測試並套用了此流程完成部署。

開發人員只需將寫好的專案 push 到 GitLab 上存放，
Jenkins 端設定的排程就會自動檢查有無更新來自動建置，
並執行 Docker 指令來完成自動部署。

demo影片:https://youtu.be/DWlC3IQXzic