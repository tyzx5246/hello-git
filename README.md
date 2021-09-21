# git 學習筆記
:::info
- ==工作目錄(Working directory)== Git 相關操作都會在這個目錄下完成
- ==暫存區(Staging area)== 放準備要提交到儲存庫的檔案
- ==儲存庫(Repository)== 是記錄檔案或目錄狀態的地方
- **:triangular_flag_on_post:每次提交檔案時** 建議(修改)小而(功能)完整


![](https://i.imgur.com/WdWsT1I.png)
git 版本控制基本架構（[來源](https://vocus.cc/article/5de3dbb8fd89780001d599fc)）
:::
- `git add <file>` 將當前位於工作目錄的檔案加入暫存區。
- `git commit -m"紀錄訊息"` 將目前位於暫存區的檔案提交到儲存庫。
- `git commit -am"紀錄訊息"` 如果檔案夾已加入「git控管」，  
 用`git commit -am` 一次完成`git add`＋`git commit -m`兩個步驟。
 
 
### :bookmark:一般檔案操作架構
```sequence
工作目錄->暫存區: git add <file>
暫存區->儲存庫: git commit -m"紀錄訊息"
```
- 加入檔案到暫存區：`git add <file>`
- 提交檔案到儲存庫：`git commit -m"紀錄訊息"`
- 查看檔案狀態：`git status`
- 查看版本紀錄：`git log`
- 檢視每筆提交簡略的統計資訊`git log --stat`

### :bookmark:操作指令
- 創建資料夾(工作目錄)：`mkdir <file>`
- 新增檔案：`touch <file>`
- 刪除檔案：`rm <file>`
- 複製檔案：`cp <file>`
- 移動檔案：`mv <file>`


### :bookmark:查看指令
- 前往資料夾：`cd <file>`
- 到目前資料夾上一層：`cd ..`
- 到目前資料夾最外層：`cd ~`
- 查看當前位置：`pwd`
- 查看當前資料夾內檔案：`ls`
- 以完整格式列出所有的檔案： `ls -al`
- 檢視檔案內容： `cat <file>`
- 清除終端機畫面：`clear`

### :bookmark:查看檔案的某一行是誰寫的 `git blame`
- `git blame <file>` 可以看到檔案的每一行是誰修改的。
- 很多時候，git blame 抓到的兇手大多都是自己！

### :bookmark:查看修改檔案的差異`git diff`
- `git diff <file>` 會顯示工作目錄和暫存區的差異。
- `git diff --cached <file>` 會顯示暫存區與儲存庫的差異。

```sequence
工作目錄->暫存區: git diff <file>
暫存區->儲存庫: git diff --cached <file>
```


### :bookmark:回復指令
- `git restore <file>` : 回復檔案上一次的修改。
- `git restore --staged <file>` : 將位於暫存區的檔案拉回到工作目錄。
```sequence
工作目錄->暫存區: git add <file>
暫存區-->工作目錄: git restore --staged <file>
```


### :bookmark:分支操作指令
- 檢視分支：`git branch`
- 建立分支：`git branch <branch name>`
- 刪除分支：`git branch -d <branch name>`
- 切換分支：`git switch <branch name>`

### :bookmark:分支合併 `merge`
- 切換到目前主分支1：`git switch <branch name1>`
- 將指定分支2合併到主分支1：`git merge <branch name2>`
- 
### :bookmark:在`github`合併分支的流程
- 在 github 發 pull request，請同事code review過，再merge。
![](https://i.imgur.com/JYVKRQL.png)


### :bookmark:`Git Flow`
![](https://i.imgur.com/XuQUXVM.png)

---

- :green_heart: Master 分支
  主要是用來放穩定、隨時可上線的版本。這個分支的來源只能從別的分支合併過來，開發者不會直接 Commit 到這個分支。因為是穩定版本，所以通常也會在這個分支上的 Commit 上打上版本號標籤。

- :blue_heart: Develop 分支
  這個分支主要是所有開發的基礎分支，當要新增功能的時候，所有的 Feature 分支都是從這個分支切出去的。而 Feature 分支的功能完成後，也都會合併回來這個分支。

- :heart: Hotfix 分支
  當線上產品發生緊急問題的時候，會從 Master 分支開一個 Hotfix 分支出來進行修復，Hotfix 分支修復完成之後，會合併回 Master 分支，也同時會合併一份到 Develop 分支。

 >>為什麼要合併回 Develop 分支？如果不這麼做，等到時候 Develop 分支完成並且合併回 Master 分支的時候，那個問題就又再次出現了。

 >>那為什麼一開始不從 Develop 分支切出來修？因為 Develop 分支的功能可能尚在開發中，這時候硬是要從這裡切出去修再合併回 Master 分支，只會造成更大的災難。

- #### :yellow_heart: Release 分支
  當認為 Develop 分支夠成熟了，就可以把 Develop 分支合併到 Release 分支，在這邊進行算是上線前的最後測試。測試完成後，Release 分支將會同時合併到 Master 以及 Develop 這兩個分支上。Master 分支是上線版本，而合併回 Develop 分支的目的，是因為可能在 Release 分支上還會測到並修正一些問題，所以需要跟 Develop 分支同步，免得之後的版本又再度出現同樣的問題。
- #### :purple_heart: Feature 分支
  當要開始新增功能的時候，就是使用 Feature 分支的時候了。Feature 分支都是從 Develop 分支來的，完成之後會再併回 Develop 分支。
  
>引用自 [Git Flow 是什麼？為什麼需要這種東西？](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)


