### <a href="https://github.com/partyyaya/GitLearning">Github 連結</a>
## git 使用指令

### 基本使用
- [git 安裝](https://git-scm.com/downloads)
- 設定 git 使用者
  - 設定名字 : git config --global user.name "名字"
  - 設定信箱 : git config --global user.email "信箱"
- 查看git設定
  - git config --global user.name
  - git config --global user.email

---
### 開始專案
  - 無原始檔案
    - 初始化 git: git init
    - 新增遠端位置: git remote add [名稱(origin)] [網址]
      - 網址可透過 github 開新專案後取得
    - 將新增內容全部加入: git add .
    - 進行初始化 commit: git commit -m init
    - 上傳遠端: git push origin master
  - 若有原始專案
    - 第一種方式: git init -> git remote add [名稱(origin)] [網址] -> git pull [名稱(origin)] [分支] 
    - 第二種方式: git clone [網址]
      - 複製他人專案分支 : git clone [網址] [分支名稱]
      - 若要觀看遠端分支資料: git checkout [遠端分支名稱(可由 git branch -r 觀看)]
        - ex: git checkout origin/experimental
      - 取得遠端分支資料(本地會多一個新分支): git checkout [遠端分支名稱]
        - ex: git checkout experimental
      - 複製單一分支: git clone --single-branch --branch [分支名稱] [遠端位置]
        - git clone -b [分支名稱] [遠端位置]
      - 更新遠端所有分支: git remote update origin --prune
      - 取得遠端資訊(若取得不到) : git fetch origin  
    
---
### 上傳常用指令
  - 查看目前狀態: git status
    - 若對單一檔案想還原到上個commit狀態: git checkout 檔案名
    - 全部還原到上一版狀態: git reset --hard
  - 加入全部到索引: git add .
  - 加入單一檔案進索引: git add 檔案名
    - 若要取消全部索引狀態: git reset HEAD 或 git reset
    - 取消單筆: git reset HEAD 檔案名 或 git reset 檔案名
  - git commit -m (版本訊息)
    - 若想修改剛剛"最新"的 commit message: git commit --amend -m 想修改的訊息
  - git push (遠端位置或名稱(origin)) (分支名稱)
  
---
### 合併分支(含遠端)
  - 先切換到主分支: git checkout [主要分支]
  - 多人合作時需先更新主要分支: git pull origin [主要分支]
  - 將分支合併到主分支: git merge [分支]
  - 將主分支資訊上傳至遠端: git push origin [主要分支]
  - 刪除遠端分支: 
    - 先刪除本地分支: git branch -d [分支]
    - 將刪除分支資訊上傳到遠端: git push origin :[分支]
  - 若合併碰到錯誤情況
    - 到該檔案進行編修
    - 加入修改: git add . 
    - 確認修改: git commit 'merge哪些東西'
    - 合併專案: git merge [分支]
    - 上傳更新: git push origin [主要分支]
    
---
### gitignore
  - 直接使用記事本新增即可(utf-8編碼存取)
    - 或使用終端機創建: touch .gitignore
  - 可以觀看個程式語言需要忽略的檔案: [gitignore](https://github.com/github/gitignore)
  - 忽略整個資料夾: 資料夾名/
  - 忽略類似附檔名檔案: *.副檔名
  - 若忽略發生錯誤使用指令矯正:
  ```
  git rm -r --cached .
  git add .
  git commit -m "fixed untracked files"
  ```

---
### git branch 常用指令
  - 查看所有遠端分支: git branch -r
    - 結束: q
  - 查看所有分支: git branch -a
    - 結束: q
  - 查看本地所有分支與所在分支: git branch
  - 刪除分支: git branch -d [分支名稱]
  - 新增 [新分支] 於 [主分支] 底下 : git branch [新分支] [主分支]
    - 主分支可加可不加，但需在主分支底下 

---
### git remote 常用指令
  - 重設遠端分支網址: git remote set-url [遠端位置名稱] [url]
  - 改變遠端位置名稱: git remote rename [原名稱] [修改名稱]
  - 查看有哪些遠端位置(使用 git clone 附有 origin): git remote -v
  - 新增遠端位置: git remote add [名稱(origin)] [網址]
  - 本地更新遠端所有資訊與分支: git remote update origin --prune

---
### git tag (git 標籤)
  - 在此版本新增標籤: git tag 標籤名稱(git tag v1)
  - 新增詳細標籤: git tag -am '敘述' 標籤名稱(git tag 'update xxxx' v1)
  - 切換到此標籤版本: git checkout v1(標籤名稱)
  - 查看所有標籤: git tag
  - 查看所有詳細標籤內容: git tag -n
    - 若沒有設定標籤內容則會自帶當初此版本commit敘述內容
  - 刪除標籤: git tag -d v1(標籤名稱)

---
### git stash (git 暫存)
  - 暫存當前版本進度: git stash
    - (Untracked 狀態的檔案預設沒辦法被 Stash，需額外使用 -u)
    - 使用完會恢復到未更改的版本(git status 會發現 nothing to commit)
  - 還原最新的暫存(最新暫存會刪除): git stash pop
    - 還原指定版本暫存: git stash pop stash@{2}
  - 不刪除暫存並套用分支上: git stash apply stash@{2} or git stash apply
  - 清除最新的暫存: git stash drop
    - 刪除指定暫存: git stash drop stash@{0}
  - 清除全部暫存: git stash clear
  - 查看目前所有暫存: git stash list

---
### git 其他使用指令
  - 切換至該版本紀錄
    - git checkout (commit前4碼，可由git log觀看)
    - 復原則直接切換到該分支即可
  - 救回不小心刪除的檔案
    - git checkout xxx.txt: 將 xxx.txt 的檔案回復到上一次的Commit的狀態
    - git checkout HEAD~2 xxx.txt:將回復到兩個版本以前的 xxx.txt
    - git checkout . :將檔案回復到上一次Commit的狀態
  - git blame index.html:查看該檔案修改的所有紀錄
  - git reflog:查看移動HEAD移動歷程(狀態每當你的HEAD有移動~他就會在這邊記上一筆)
