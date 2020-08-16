---
title: "我把 Hugo 部落格部署在 GitHub 上"
author: "Marco Lee"
date: 2020-08-15T15:46:23+08:00
description: 記錄在 GitHub 部署 Hugo 的過程
tags: ["Hugo", "Hugo Themes", "Homebrew", "GitHub"]
---
我想要重新開張個人部落格，選擇了 Hugo。最大的原因是它可以直接架在 GitHub 上，而且輕盈簡潔，號稱 `"The world’s fastest framework for building websites"`。不像 Wordpress，還得為它找一個虛擬主機；儘管我比較熟悉 Wordpress，還是決定試試 Hugo。其背後隠藏的原因是... GitHub 和 Hugo 都免費。哈哈。

我使用 MacOS。部署 Hugo 到 GitHub 分為兩個部份，我處理的過程如下：

### 一、本地建立檔案

#### 1. 安裝 Homebrew。
打開**終端機**，將下一行命令複製貼到**終端機**執行<cite>安裝[^1]</cite>。
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
[^1]: Homebrew 官方網站網址如右：<https://brew.sh/>。

#### 2. 安裝 Hugo
直接下達指令安裝 Hugo。Hugo 有完整詳細的說明文件，有時間再來仔細<cite>瞧瞧[^2]</cite>。

```sh
$ brew install hugo
```
[^2]: Hugo 官方網站網址如右：<https://gohugo.io/>。

#### 3. 建立新網站
下達指令建立新網站，並指定網站名稱。與網站同名的資料夾為部落格網站的根目錄。切換到資料夾內，等待下一步的處理步驟。

```sh
$ hugo new site website-hugo
$ cd website-hugo
```
>我的新網站名稱採用和 GitHub 帳戶相同的名稱。你不一定得這麼做，可以替換成任意名稱。進入新網站同名的新資料夾，觀察一下內部資料夾結構。

現在的資料夾結構應如下所示：
```
.
├── archetypes
├── content
├── data
├── layouts
├── static
├── themes
└. config.toml
```

#### 4. 選擇並套用佈景主題
在網站根目錄複製中意的佈景主題到下一層 themes 資料夾內。在官方的 [Hugo Themes](https://themes.gohugo.io/) 網頁上有很多佈景主題可供挑選。

```sh
$ git clone https://github.com/spf13/hyde.git themes/hyde
```
我們可以下載多個佈景主題，在 Hugo Themes 網頁進入到中選的佈景主題頁面，可找找到相關的說明。比照上述指令將佈景主題的 repository 複製到 *themes/佈景主題名稱* 資料夾中。

接下來，在 config.toml 檔案中，將 hyde 指定為預設的佈景主題，加入的指令如下：
```
theme = "hyde"
```
再將 /themes/hyde 中的 static 和 layouts 資料夾複製到根目錄，取代原來的 static 和 layouts 資料夾。
>稍後，我會再記錄如何更換另一個佈景主題，也就是更換為目前使用的佈景主題。

##### Hyde 佈景主題外觀如下。圖片連結自 <https://themes.gohugo.io/hyde/>。此頁面有詳細的介紹及使用說明。
![Themes](https://f.cloud.github.com/assets/98681/1831229/42b0b354-7384-11e3-8462-31b8df193fe5.png "Hugo Themes,Hyde")

#### 5. 編輯 config.toml
使用編輯器開啟根目錄中的 config.toml；我使用 Visual Studio Code，調整內容大致如下：

```
baseURL = "https://your-account.github.io/"    # 更改 GitHub 帳號名稱
languageCode = "zh-tw"                         # 設定使用繁體中文
title = "Blog of someone"
theme = "hyde" 
```

#### 6. 建立新文章頁面
上述步驟已經完成了 Hugo 的架設。若要建立新文章頁面，必須使用 hugo new 指令，如下：

```sh
$ hugo new posts/my-first-post.md
```
此指令會在 /content/posts 資料夾中建立 my-first-post.md 頁面。使用編輯器打開此頁面，將 draft 的參數由 true 改成 false，如下；或者把這一行刪除。

```
---
title: "My First Post"
date: 2020-08-15T15:46:23+08:00
draft: false
---
```

>Hugo 頁面使用 <cite>Markdown[^3]</cite> 語言編輯，我需要再花點時間了解其語法，並找尋適當的編輯工具，以編輯出好看好讀的頁面。我目前暫時使用 Visual Studio Code。

[^3]: Markdown 官方網站網址如右：<https://daringfireball.net/projects/markdown/>。另一個 Markdown Guide 網站也提供了不少實用的資訊 <https://www.markdownguide.org/>。

#### 7. 進行本地端測試
啟動 Hugo 伺服器，指令如下。針對到此的成果進行本地端測試。
```sh
$ hugo server -D
```
伺服器啟動後，在瀏覽器中輸入網址 http://localhost:1313，網站便呈現在眼前。

>到目前為止，我們已經可以在本地端測試 Hugo 部落格。在本地端伺服器啟動的狀態下，我們修改文章頁面，或新增文章頁面，都會即時更新狀態。

#### 8. 更換佈景主題
佈景主題存放在 themes 資料夾內。可以分別存放多個佈景主題。目前本網站使用的佈景主題是 <cite>anatole[^4]</cite>，可以執行下列指令將佈景主題複製下來。

[^4]: anatole 頁面網址如右：<https://themes.gohugo.io/anatole/>。

```sh
$ git clone https://github.com/lxndrblz/anatole.git themes/anatole
```
接下來需要調整 config.toml 檔案，通用的設定如下列四項。最好的方法是複製 themes/anatole/exampleSite 資料夾內的 config.toml 來修改。詳細的調整方法請參考 [Anatole](https://themes.gohugo.io/anatole/) 頁面內的說明。
```
baseURL = "https://your-account.github.io/"    # 更改 GitHub 帳號名稱
languageCode = "zh-tw"                         # 設定使用繁體中文
title = "Blog of someone"
theme = "anatole" 
```
接下來將 themes/anatole/exampleSite 資料夾內的 content 和 static 兩個資料夾，複製到根目錄覆蓋原有的同名資料夾。

最後啟動 Hugo 伺服器進行本地端測試。

![screenshot](/images/tn.png "anatole")

### 二、發佈 Hugo 到 GitHub

#### 1. 在 GitHub 建立兩個 repository
在 GitHub 建立 your-account.github.io 和 website-hugo 兩個 repository。

#### 2. 建立 public 資料夾
我們在本地端建立的頁面，測試完畢後，需要打包到 public 資料夾，然後發佈到 GitHub。打包的方法便是下達 hugo 指令，如下：

```sh
$ hugo
```
#### 3. 將 Hugo 發佈到 GitHub 上
將 public 資料夾發佈到 GitHub 上的 your-account.github.io。需要切換到 public 資料夾。按下列指令執行：

```sh
$ cd public
$ git init
$ git remote add origin https://github.com/your-account/your-account.github.io.git
$ git add .
$ git commit -m "push public"
$ git push -u origin master
```

回到根目錄，把整個根目錄發佈到 GitHub 上的 website-hugo。按下列指令執行：
```sh
$ cd ..
$ git init
$ git remote add origin https://github.com/your-account/website-hugo.git
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```
#### 4. 打開瀏覽器輸入網址 https://your-account.github.io

>大功告成