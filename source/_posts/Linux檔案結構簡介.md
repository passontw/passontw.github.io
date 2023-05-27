---
title: Linux檔案結構簡介
date: 2021-09-07 17:40:37
tags:
  - Linux
---

# Linux

因為之後會部署在 Linux 上

所以要先大概了解一下檔案結構

[鳥哥的 Linux 私房菜](http://linux.vbird.org/linux_basic/)

# 檔案結構

[File stem Hierarchy Standard](https://zh.wikipedia.org/wiki/%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84%E6%A0%87%E5%87%86)

Linux 檔案結構是樹狀的結構

![image](https://i.iter01.com/images/fea26b1f0428e5e32782529bf0321113b273cbf308cdd281e2f9088efdbe7cc7.png)

檔案資料夾的部分可以參考鳥哥的文章

這裡只挑選幾個常用的資料夾

## /home

這是系統預設的使用者家目錄(home directory)

在你新增一個一般使用者帳號時

預設的使用者家目錄都會規範到這裡來

比較重要的是，家目錄有兩種代號喔: 

* ~: 代表目前這個使用者的家目錄
* ~dmtsai : 則代表 dmtsai 的家目錄

## /root

系統管理員(root)的家目錄

之所以放在這裡，是因為如果進入單人維護模式而僅掛載根目錄時， 該目錄就能夠擁有root的家目錄

所以我們會希望root的家目錄與根目錄放置在同一個分割槽中。

## /lib

系統的函式庫非常的多

而/lib放置的則是在開機時會用到的函式庫

以及在/bin或/sbin底下的指令會呼叫的函式庫而已

什麼是函式庫呢？妳可以將他想成是『外掛』，某些指令必須要有這些『外掛』才能夠順利完成程式的執行之意

另外 FHS 還要求底下的目錄必須要存在: 

* /lib/modules/: 這個目錄主要放置可抽換式的核心相關模組(驅動程式)喔

## /etc
系統主要的設定檔幾乎都放置在這個目錄內

例如人員的帳號密碼檔、 各種服務的啟始檔等等。

一般來說，這個目錄下的各檔案屬性是可以讓一般使用者查閱的， 但是只有root有權力修改

FHS建議不要放置可執行檔(binary)在這個目錄中喔

比較重要的檔案有:  `/etc/modprobe.d/` `/etc/passwd` `/etc/fstab` `/etc/issue` 等等

另外 FHS 還規範幾個重要的目錄最好要存在 /etc/ 目錄下喔: 

* /etc/opt(必要): 這個目錄在放置第三方協力軟體 /opt 的相關設定檔
* /etc/X11/(建議): 與 X Window 有關的各種設定檔都在這裡，尤其是 xorg.conf 這個 X Server 的設定檔。
* /etc/sgml/(建議): 與 SGML 格式有關的各項設定檔
* /etc/xml/(建議): 與 XML 格式有關的各項設定檔

## /usr

usr 並不是 user 的縮寫

而是 `Unix Software Resource` 的縮寫

意思是 Unix 作業系統軟體資源放置的地方

而不是使用者的資料夾

而更細節的資訊可以參考 鳥哥看更多的解說

## /var

/var目錄主要針對常態性變動的檔案

包括快取(cache)、登錄檔(log file)以及某些軟體運作所產生的檔案

包括程序檔案(lock file, run file)

或者例如MySQL資料庫的檔案等等

## /tmp

這個目錄是用來存放一些臨時檔案的。

# 目錄樹

在Linux底下，所有的檔案與目錄都是由根目錄開始的

那是所有目錄與檔案的源頭

然後再一個一個的分支下來

有點像是樹枝狀啊

我們也稱這種目錄配置方式為: 目錄樹(directory tree)

主要的特性有: 

* 目錄樹的啟始點為根目錄 (/, root)
* 每一個目錄不止能使用本地端的 partition 的檔案系統，也可以使用網路上的 filesystem 。舉例來說， 可以利用 Network File System (NFS) 伺服器掛載某特定目錄等
* 每一個檔案在此目錄樹中的檔名(包含完整路徑)都是獨一無二的

# 絕對路徑與相對路徑

所謂的路徑(path)定義為絕對路徑(absolute)與相對路徑(relative)

這兩種檔名/路徑的寫法依據:

* 絕對路徑: 由根目錄(/)開始寫起的檔名或目錄名稱， 例如 /home/dmtsai/.bashrc
* 相對路徑: 相對於目前路徑的檔名寫法。 例如 `./home/dmtsai` 或 `../../home/dmtsai/` 等等。反正開頭不是 / 就屬於相對路徑的寫法

接下來在處理一下網頁伺服器 (Nginx)
