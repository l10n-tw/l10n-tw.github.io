---
title: Git 教學
permalink: /development/git.html
---

Git 是個分散式的版本控制系統  
以往的版本控制系統都是將程式碼放在伺服器上集中管理  
當修改程式碼時皆需要連上網路，將修改一一提交  
而 Git 則可以不需要連上網路，來做單機的版本控制  
除了單機也能透過伺服器代管程式碼提交回去  

首先如果要使用 Git  
要在專案資料夾下

* 初始化  

        git init // 這是讓 git 初始化，生成 .git/ 資料夾

* 加入追蹤  
    接著專案資料夾底下，應該有了一些檔案，為了讓 git 去追蹤這個檔案必須使用 git add 加入追蹤。

        git add file_name

    或者想將該資料夾底下所有檔案/資料夾都加入追蹤可以用 * 代表全部

        git add *

* 顯示狀態  
    當完成這些動作時，可以使用 git status 來查看追蹤的狀態

        git status

    在還沒加入追蹤前可能會顯示 Untracked

* 提交修改  
    當我們做完小幅度的修改時，這時理所當然就是要將檔案提交出去，當作一個小小的版本
    這時我們可以使用 git commit 將修改送出並且紀錄下來

        git commit // 如果沒有加參數則會跳到文字編輯器的畫面請你加入文字說明
        git commit -m "修改的文字說明" // -m 是要將文字說明也一併紀錄
        /*
         * 到了後來會進行多個檔案的修改，這時候 commit 可能會出現錯誤的訊息
         * 原因是因為你要將所有修改過的檔案都提交，所以要嘛就是針對單一檔案提交
         * 不然就是加上參數，讓所有被修改過得檔案一口氣提交
         */
        git commit file_name 對單一個尚未提交的檔案進行提交
        git commit -a -m "文字說明"


* 基本流程  
    基本上做版本控制幾乎只有兩件事情要做

    * add
    * commit

    這兩件事就是不斷的讓 Git 幫你對檔案做追蹤

* 回復檔案  
    說到回復檔案必須先對 Git 中的 HEAD 做個說明， HEAD 在 Git 中代表最近一次的 commit
    因此 Git 利用一些表示方法來代表前幾次的 commit

        HEAD (最近一次的 commit，可以想像就是現在的 commit）
        HEAD^ (上一次的 commit)
        HEAD~2 (上上一次 的 commit)
        HEAD~3 (上上上一次的 commit)
        其餘以此類推

    而回復的指令為 git reset ，而 reset 有分軟性的回覆跟硬性的
    * 軟性: 不會把新增或刪除的文字給刪除，單純殺掉 commit 而已（通常 commit 文字訊息打錯，可以用軟性回復，再重新提交一次)
    * 硬性: 除了將 commit 給殺掉之外，也會將文字變回原樣，這要看是回復到哪一次的 commit 而定

            使用方法: git reset 提交的版本
            軟性:
                git reset HEAD^ // 將 commit 切到上一次提交的狀態
                                // 但刪修過得文字不會移除，不加上參數預設為軟性
                git --soft reset HEAD~2 // 同樣是軟性，這次是切換到上上次提交的狀態

            硬性:
                git --hard reset HEAD // 可以將文字變回最近這次 commit
                git --hard reset HEAD^ // 將這次的 commit 殺掉
                                       // 切回上一次的 commit 之外
                                       // 會將文字變成上一次 commit 的樣子

* 使用 GitHub  
    Git 除了可以單機做版本控制，也能找個代管伺服器來做版本控制，而 GitHub 則是目前最夯的代管商，
    目前只要程式碼是 Open 給大家的，都可以免費使用 GitHub

    首先註冊完 GitHub 的帳號之後，點 New Repository ，這時候會要求你輸入一個名稱，可以使用自己的專案名稱，接著到了下一頁之後，會有告訴你將專案上傳到 GitHub 的方法

        Create a new repository on the command line
        (還沒有專案的話，這會教你如何創新專案)

        touch README.md // 只是創造說明文件
        git init // 這就是初始化啦
        git add README.md (將 README.md 加入追蹤)
        git commit -m "first commit" (第一次 commit)
        git remote add origin https://github.com/user_name/xxx.git (新增一個要遠端代管的位置，這當然是 GitHub 給的網址囉)
        git push -u origin master (將專案送上伺服器)

        接著會要求你 GitHub 的帳號密碼，輸入完就會送上 GitHub 囉

    當然，如果你已經有一個現成的，可以更快的丟到 GitHub 上

        Push an existing repository from the command line
        (已經有現成的專案)

        git remote add origin https://github.com/FreedomKnight/test.git
        git push -u origin master
        一樣會要求你輸入帳號密碼

    如果要跟人家合作開發的話，有幾件事情要做，如果是要讓人來參與的話，可以將對方的 GitHub 帳號加進 Collaborator (Setting -> Collaborators -> 新增朋友帳號)

    如果是要參與人家的專案的話，第一件事情就是將對方的專案給複製過來

        git clone 網址 // 這會將人家 GitHub 上的專案給複製下來

        開發流程:
        git pull // 這會去檢查你複製過來的專案有沒有其他人提交新的 commit
                 // 如果有的話就會幫你更新複製過來的專案
        git commit -a -m "xxxx" // 總之就是提交你的修改，但這時提交會是在本機上
        git push // 將現在所有的提交推送回伺服器

        接著下一次修改，又從 pull 開始
