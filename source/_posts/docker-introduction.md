---
title: Docker 簡介
date: 2021-11-07T09:52:36.000Z
tags: docker
category: docker
---

![logo](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/1220px-Docker_%28container_engine%29_logo.svg.png)

# 基本介紹 <!-- markdownlint-disable MD025 -->

[Docker](https://www.docker.com/) 是一個開源專案，出現於 2013 年初，最初是 Dotcloud 公司內部的 Side-Project。

它基於 Google 公司推出的 [Go](https://golang.org/) 語言實作。（ Dotcloud 公司後來改名為 Docker ）

## Docker 是什麼？

Docker 是一種[容器](https://containerd.io/)，而容器是打包代碼及其所有依賴項的標準軟件單元，因此應用程式可以從一個計算環境快速可靠地運行到另一個計算環境。

不太明白？沒關係，我們先來看看 Docker 能夠替我們解決什麼問題。

- 簡化建置環境的麻煩

- 不同平台的相容性

以往在開發之前都要去安裝一大堆套件之後，才能夠開始寫 code

例如：開發前端就要裝 `node` 、開發後端可能就要安裝一個後端語言或是資料庫

依照使用的套件的不同，還得再安裝其他不同的相依的環境

最頭痛的是，使用不同電腦、不同作業系統，安裝的流程也不盡相同

像是 `Ubuntu` 和 `Centos` 的安裝指令以及可安裝的套件皆不同，更別提 `Windows` 了

因此會常常遇到我在我的電腦上面寫好一隻程式，但搬到你的電腦上面後就變得不能夠執行了，這種尷尬的問題。

## 容器 vs 虛擬機

在容器出來之前，講到虛擬化技術就會想到虛擬機，其中又以 [VMware](https://www.vmware.com/tw.html) 和 [VirtualBox](https://www.virtualbox.org/) 最具代表。而現在講到容器，又以 Docker 最有名。

但兩者之間有存在一些不同之處，可以用下圖來做比較。

![vm](https://miro.medium.com/max/1400/0*fQKhoT--2NnLY9YU.png)

虛擬機器是在系統層上虛擬化，透過 [Hypervisor](https://zh.wikipedia.org/wiki/Hypervisor) 在目標的機器上提供可以執行一個或多個虛擬機器的平台，而這些虛擬機器可以執行完整的作業系統。

簡單來說，Hypervisor 就是一個可以讓你在作業系統（Host OS）上面再裝一個作業系統（Guest OS），然後讓兩個作業系統彼此不會打架的平台。

所以我們可以在 Mac 電腦上面用虛擬機執行 Windows 的作業系統，反之亦然。

![container](https://miro.medium.com/max/1400/0*bL7e7IJ5s-ntdhvC.png)

容器是在[作業系統層上虛擬化](https://zh.wikipedia.org/wiki/%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1%E5%B1%A4%E8%99%9B%E6%93%AC%E5%8C%96)，透過 Container Manager 直接將一個應用程式所需的程式碼、函式庫打包，建立資源控管機制隔離各個容器，並分配 Host OS 上的系統資源。透過容器，應用程式不需要再另外安裝作業系統（Guest OS）也可以執行。

由於不用再安裝作業系統（Guest OS），所以容器對比虛擬機有些優勢：

功能     | 容器        | 虛擬機
------ | --------- | -----
啟動時間   | 秒級        | 分鐘級
容量     | MB        | GB
效能     | 接近原生      | 比較慢
系統支援量  | 單機支援上千個容器 | 一般幾十個
複製相同環境 | 快         | 慢
隔離性    | 較差        | 較好

但又因為虛擬機有 Hypervisor，所以比起容器擁有更好的隔離性，其他部份則是容器比較有優勢。

## 使用 Docker 的好處

- 更快速的交付和部署

  對開發和維運（DevOps）人員來說，最希望的就是一次建立或設定，可以在任意地方正常執行。

  開發者可以使用一個標準的映像檔來建立一套開發容器，開發完成之後，維運人員可以直接使用這個容器來部署程式碼。 Docker 可以快速建立容器，快速迭代應用程式，並讓整個過程全程可見，使團隊中的其他成員更容易理解應用程式是如何建立和工作的。 Docker 容器很輕很快！容器的啟動時間是秒級的，大量地節約開發、測試、部署的時間。

- 更有效率的虛擬化

  Docker 容器的執行不需要額外的虛擬化支援，它是核心層級的虛擬化，因此可以實作更高的效能和效率。

- 更輕鬆的遷移和擴展

  Docker 容器幾乎可以在任意的平台上執行，包括實體機器、虛擬機、公有雲、私有雲、個人電腦、伺服器等。 這種兼容性可以讓使用者把一個應用程式從一個平台直接遷移到另外一個。

- 更簡單的管理

  使用 Docker，只需要小小的修改，就可以替代以往大量的更新工作。所有的修改都以增量的方式被分發和更新，從而實作自動化並且有效率的管理。

## 結語

Docker 的 Logo 設計成鯨魚跟貨櫃，是希望工程師開發的應用程式，能夠像貨櫃屋一般，可以很彈性的搬遷，隨放即用。
