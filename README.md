# WordCamp Taiwan 2021 佈景主題

WordCamp Taiwan 2021 活動網站樣式開發。
本專案是來自 [WordCamp Taipei 2019](https://github.com/wordcamp-taiwan/WCTPETW) 的分支專案。

## 活動網站本地測試

### 本地端主機測試安裝

可參考 **主要官方網站本地端主機測試安裝** 或是使用你習慣的本地 WordPress 測試環境

### 安裝 WordCamp Taipei 2021 主題

1. 確定已安裝 Twenty Seventeen 主題
2. 利用終端機 (macOS) 或命令提示字元 (Windows) 執行 `cd /path/to/your/WordPress/wp-content/themes`，並複製 WordCamp Taipei 2021 主題到本機 `git clone git@github.com:wordcamp-taiwan/wctw2021.git`
3. 啟用 WordCamp Taipei 2021 主題

### 建立開發環境

1. 確認系統中已安裝 [Node.js](https://nodejs.org/en/)
2. 在佈景主題路徑 (`wctw2021`) 中執行 `npm install` (如果權限不夠請用 `sudo npm install`)。這會安裝所有方便開發的工具：[gulp](https://gulpjs.com/), [livereload](https://www.npmjs.com/package/gulp-livereload), [autoprefixer](https://github.com/postcss/autoprefixer), [cssnano](https://cssnano.co/)
記得安裝 [livereload 瀏覽器擴充套件](http://livereload.com/extensions/)，每次更新 CSS 檔案後，瀏覽器會自動刷新。

- `npm run build` 只跑一次
- `npm run watch` 會持續監控 CSS 檔案

主要修改檔案 /src/style.css
輸出檔案 /dest/style.css

### 建立提取要求 (Pull Request)
1. 在本專案中按下右上角的 \[Fork\] 建立分支專案。
2. 利用終端機 (macOS) 或命令提示字元 (Windows) 執行 `cd /path/to/your/WordPress/wp-content/themes/wctw2021`，在佈景主題路徑中執行 `git remote origin set-url {{你的 Git 存放位址.git}}`
3. 接著執行 `remote add upstream git@github.com:wordcamp-taiwan/wctw2021.git`。
4. 每次開發前，先執行 `git pull upstream main` 更新最新版本
5. 在本地編輯完後，建立本地版本 `git add . && git commit -m "版本資訊"`，並執行 `git push origin main` 將版本推送到自己的 Git 存放庫。
5. 前往 [Pull Request](https://github.com/wordcamp-taiwan/wctw2021/pulls) 頁面，點擊 \[New Pull Request\]。
6. 點擊 \[compare across forks\]，將右邊的 Repo 改為自己的 repo。
7. 按照介面提示，逐步建立提取要求，並通知網站組夥伴進行測試與合併。

## 主要官方網站本地測試

### 本地端主機測試安裝

本地端測試環境需求：
- [VirtualBox 5.x](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant 2.1+](https://www.vagrantup.com/downloads.html)
- [Varying Vagrant Vagrants (VVV)](https://varyingvagrantvagrants.org/)
- [WordPress Meta Environment](https://github.com/WordPress/meta-environment)

安裝步驟：
1. 安裝 [VirtualBox 5.x](https://www.virtualbox.org/wiki/Downloads)
2. 安裝 [Vagrant 2.1+](https://www.vagrantup.com/downloads.html)
3. 確認安裝 Vagrant `vagrant -v` 檢查版本
4. 安裝 hosts 自動更新插件 `vagrant plugin install vagrant-hostsupdater`
5. 用 `git` 安裝 VVV `git clone -b master git://github.com/Varying-Vagrant-Vagrants/VVV.git ~/vagrant-local`
6. `vagrant up` 啟動 VVV 確認 http://vvv.test/ 是否有確實執行
7. 找到 `vvv-custom.yml` 檔案。
   如果沒有請複製 `vvv-config.yml` 並建立 `vvv-custom.yml` 檔案。 `cp vvv-config.yml vvv-custom.yml`
8. 請把這幾行 uncomment
   ```yml
   #wordpress-meta-environment:
   #  repo: https://github.com/WordPress/meta-environment.git
   ```
9. 複製貼上以下內容，不需要的網站可以改成 `false` 才不會啟動安裝跑太久。
   ```yml
   wordpress-meta-environment:
   description: "An environment useful for contributions to the WordPress meta team."
   repo: https://github.com/WordPress/meta-environment.git
   hosts:
     - wp-meta.test
   custom:
     provision_site:
       "buddypressorg.test": true
       "jobs.wordpressnet.test": true
       "wordcamp.test": true
       "wordpressorg.test": true
       "wordpresstv.test": true
   ```
10. 重新啟動 VVV
    `vagrant reload --provision`
11. 檢查 http://wp-meta.test 是否成功，主要 WordCamp 測試網站為：http://central.wordcamp.test/

### 安裝 WordCamp Taipei 2019 主題

`cd /vagrant-local/www/wordpress-meta-environment/wordcamp.test/public_html/wp-content/themes/`
1. pull WordCamp Taipei 2021 主題 `git clone git@github.com:wordcamp-taiwan/wctw2021.git`
2. 啟用 WordCamp Taipei 2021 主題
3. 去 [WordCamp Taipei 2021 網站](https://taiwan.wordcamp.org/2021/wp-admin/export.php) Tools 匯出 xml 檔案
4. Tools > Import > Run WordPress Importer (download and import attachment)
5. Appearance > Customize > Site Identity - 設定網站標題及標語
6. Appearance > Customize > Homepage settings - 設定 Homepage & Post page
7. Appearance > Customize > Menu - 設定剛剛匯入的選單
8. Appearance > Customize > Widgets - 設定 Post page 側邊欄小工具 & 頁尾 Footer
9. Appearance > Customize > Theme options - Page layout: 1 column
10. Appearance > Customize > Theme options - 設定首頁區塊
11. Appearance > Fonts >
    * Google Web Fonts: `@import url('https://fonts.googleapis.com/css?family=Noto+Sans+TC|Roboto&display=swap');`
    * Font Awesome: `https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css`
    * Check "Enqueue Dashicons"


