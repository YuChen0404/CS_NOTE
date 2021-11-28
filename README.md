CS_NOTE<a name="TOP"></a>
===================
 - - - -

## Linux背景介紹與指令實作 ##

<details>
  <summary>檔案命名原則、副檔名</summary>
  <p>:o:256個字元、字母、數字、"."(點)、"_"(下劃線)和"-"(連字元)</p>
  <p>:x:"?"(問號),"*"(星號), " "(空格), "$"(貨幣符), "&", 擴號, "/" (斜線)，"." , ".." </p>
</details>

<details>
  <summary>絕對/相對路徑的移動</summary>
  <p>絕對路徑：路徑的寫法『一定由根目錄 / 寫起』</p>
  <p>相對路徑：路徑的寫法『不是由 / 寫起』</p>
  
  指令 | 作用
------------- | -------------
cd  | 	變換目錄
pwd  | 	顯示目前的目錄
mkdir  |  建立一個新目錄
rmdir  |  刪除一個裡面是空的空目錄
cp  |  複製
mv  |  移動
ls  |  顯示目錄下的所有內容
cat  |  查看檔案內容
</details>

<details>
  <summary>編輯文檔</summary>
  
  * nano
      * Ctrl C：顯示游標所在
      * Ctrl W：查詢命令，按下後會跳轉到末行的反白位置，輸入要查詢的內容在回車及可。
  * vi/vim(vim相當於vi的升級版)
      * 一般模式
      * 編輯模式
      * 命令列模式
  
  指令 | 作用 | 指令 | 作用
------------- | -------------|------------- | -------------|
:w  | 	將編輯的資料寫入硬碟檔案中|:wq  | 	儲存後離開(若為 :wq! 則為強制儲存後離開) 
:w!  | 	若檔案屬性為『只讀』時，強制寫入該檔案|:w[filename]  | 	將編輯的資料儲存成另一個檔案（類似另存新檔）
:q  | 	離開|:r[filename]  | 	在編輯的資料中，讀入另一個檔案的資料
:q!  | 	強制離開不儲存檔案|:set nu | 	顯示行號，設定後會在每一列的自首顯示該列的行號
</details>

<details>
  <summary>檔案系統目錄結構</summary>
  <p>/.（根目錄）：所有的檔案皆從根目錄開始，只有root使用者具該目錄的許可權</p>
  <p>/root：此目錄為系統管理員，也稱作超級許可權者的使用者主目錄</p>
  <p>/bin：存著經常使用的指令</p>
  <p>/boot:系統啟動時必須讀取的檔案，包括系統核心、連線檔案以及映象檔案</p>
  <p>/dev：存放周邊設備代號的檔案</p>
  <p>/etc：放置與系統設定、管理相關的檔案</p>
  <p>/home：存放普通使用者的主目錄，在Linux中每個使用者都有一個自己的目錄，一般該目錄名是以使用者的帳號命名的</p>
  <p>/media：可用來做為光碟、軟碟片、隨身碟與其他分割區的自動掛載點</p>
  <p>tmp：供全部使用者暫時放置檔案的目錄</p>
  <p>/usr：為非常重要的目錄，使用者的很多應用程式和檔案都放在此目錄下，類似windows下的program files目錄</p>
  <p>/var：系統執行時，內容經常變動的資料或暫存檔（log file）,都會放置在這個目錄裡</p>
</details>

<details>
  <summary>更改使用者權限</summary>
  <p>ls -l：可查看每個檔案與目錄的擁有者與群組</p>
  <p>chown：可修改檔案或目錄擁有者及群組</p>
  <p>chomd：可控制檔案如何被他人調用</p>
  <p>mode：許可權設定字串</p>
</details>

<details>
  <summary>壓縮檔案</summary>
  
  * 為什麼要壓縮
      * 備份資料時方便整理
      * 將檔案變小，節省電腦硬碟的空間
      * 將無數個散亂的檔案打包成一個較小的檔案，亦方便資訊在網路上流通
      * 壓縮檔案時可視情況進行加密
  * 壓縮考慮的因素
      * 壓縮率，能夠將檔案壓到多小
      * 解壓縮所需的時間，也就是需要的CPU計算量
      * 解壓縮所需的記憶體空間
      * 相容性，解壓縮程式的普遍性
  * 壓縮的選擇
      * gzip：需要在記憶體很小、很簡單、沒什麼工具的機器解壓縮時
      * xz：需要節省網路頻寬、縮短下載所需時間時
      * tar.xz：需要最好的壓縮率時

 
 \ | gzip | xz | tar.xz
------------- | -------------|------------- | -------------|
壓縮  | 	gzip FileName| xz -z FileName| 	tar -zcvf FileName.tar.gz DirName
解壓縮  | 	gunzip FileName.gz OR gzip -d FileName.gz| xz -d FileName.xz | 	tar -zxvf FileName.tar.gz
</details>

<details>
  <summary>檔案搜尋</summary>
  
  * find [path] [option] [action] filename
      * option
          * -size
          * -name
          * -type
          * -user
      * action -exec
          * ls
          * print
  * which filename
      * -n<文件名長度>指定文件名長度，指定的長度必須大於或等於所有文件中最長的文件名
      * -p<文件名長度>與-n參數相同，但此處的<文件名長度>包括了文件的路徑
      * -w指定輸出欄位的寬度
      * -v顯示版本訊息
 </details>
  
<details>
  <summary>檔案內容查閱</summary>
  
  * cat 從第一行顯示檔案內容、形成新檔案
      * cat -n file1 > file2→把file1的檔案內容加上行號後輸入file2檔案
          * -n→由1開始對所有輸出的行數編號
          * ">"→將多個文件覆蓋到目標文件中
          * ">>"→將多個文件追加到目標文件中
  * tac 從最後一行開始顯示
      * tac -t -s 'x\|[^x]' test.log→一個接著一個字符的反轉一個文件
          * -r→將分隔符作為基礎正規表達式處理
          * -s→使用String作為分隔符代替默認的換行符
  * more 一頁一頁的顯示檔案內容
      * more +20 testfile→從第20行開始顯示testfile的文檔內容
          * ENTER：向下n行(default為1行)
          * Ctrl+F/SPACE：向下滾動一屏
          * Ctrl+B：返回上一屏
  * less 與 more 類似，顯示檔案室允許用戶既可以向前又可以向後翻頁閱讀檔案
      * ps -ef |less→ps查看進程信息並通過less分頁顯示
          * j→下一行
          * k→上一行
          * G→移動到最後一行
          * g→移動到第一行
  * head/tail 只看頭/尾巴幾行
      * head -n 20 state.txt | tail -10→顯示11~20行的內容
 </details>
 
<details>
  <summary>資料傳輸</summary>
  <p>資料傳輸階層![image](https://user-images.githubusercontent.com/80245218/143773732-b4db162e-8b31-4078-b162-4fca17665885.png)</p>
  * Port
  <p>通訊埠號是TCP/UDP與上層通訊的通道，當TCP/UDP要傳送訊息時，會指定要由哪一個通訊埠號來接收。</p>
  * TCP/IP
  <p>TCP/IP提供了點對點的連結機制，將資料應該如何封裝、定址、傳輸、路由以及在目的地如何接收，都加以標準化。</p>
</details>
  
<details>
  <summary>網路相關</summary>
  
  * route

  指令 | 作用 | 指令 | 作用
------------- | -------------|------------- | -------------|
add  | 新增一條路由規則	|target  | 目的網路或主機
del  | 刪除一條路由規則|netmask | 目的地址的網路掩碼
-net  | 目的地址是一個網路|gw | 	路由資料包通過的閘道器
-host  | 目的地址是一個主機|dev | 	為路由指定的網路介面

  * ping

  指令 | 作用 | 指令 | 作用
------------- | -------------|------------- | -------------|
-n  | 參數指定封包數|-c  | 指定Ping次數
-t  | 持續監看網路是否正常|-s  | 指定發送的數據字結數
-4/-6  | IPv4/IPv6|-i  | 指定收發資訊間隔時間
  
  * netstat
      * netstat -a|grep 3306：查看端口是否被占用
      * netstat -s：查看數據包統計信息
      * netstat -r：查看路由信息
  
  * 影響網路速度的因素
      * 延遲(Latency)：封包從來源端至目的端中間所花的時間
          * propagation delay：封包在網路線上傳輸所花費的時間，與網路線上電子訊號跑的速度有關
          * transmission delay：網路卡將資料傳送到網路線上所花的時間，與網路設備的傳送速度有關
          * nodel processing delay：路由器處理封包表頭、檢查位元資料錯誤與尋找配送路徑所花費的時間
          * queuing delay：路由器因為某些因素無法立刻將封包傳送到網路上造成封包暫存在佇列中等待的時間
      * 頻寬(Bandwidth)：傳輸媒介的最大吞吐量
</details>
