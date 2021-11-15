---
title: Docker 基本概念
date: 2021-11-13 20:31:23
tags: docker
---

今天來聊聊 Docker 的一些基本概念以及 Docker 的架構。

<!-- more -->

# Docker 三元素 <!-- markdownlint-disable MD025 -->

在 Docker 中，有幾個基本的名詞，分別是：

1. 映像檔（Image）
2. 容器（Container）
3. 倉庫（Repository）

比喻來說，映像檔就如同作業系統安裝光碟，可以重複在不同的電腦上安裝，而每一台安裝後的電腦就可以想像成是容器，最後倉庫則是從放光碟的盒子。

## 映像檔

Docker 映像檔是一個模板，用來重複產生容器實體。

例如：一個映像檔可以是一個單純的作業系統，或是包含資料庫的服務，又或者是 Python 的執行環境。

## 容器

容器則是利用映像檔執行後的一個實例，一個映像檔可以同時啟動多個容器。它可以被啟動、開始、停止、刪除，且每個容器都是相互隔離的。

例如：我們可以拿 `Ubuntu` 的映像檔來同時啟動多個容器來進行不同的操作，又或者拿 `MySQL` 的映像檔來啟動多個容器來建立資料庫叢集。

## 倉庫

倉庫（Repository）是集中存放映像檔檔案的地方，而倉庫註冊伺服器（Registry）上則存放著多個倉庫，概念就如同 GitHub 與 Repository。

倉庫註冊伺服器有分公有以及私有，最大的公有倉庫註冊伺服器則是 [Docker Hub](https://hub.docker.com/)，上面存放了數量龐大的映像檔供使用者下載。

使用者也可以在自己的電腦上面建立自己的倉庫註冊伺服器。

而 Docker 的倉庫註冊伺服器與 [git](http://git-scm.com/) 的操作類似，都是透過 `push`, `pull` 指令來上傳以及下載。

# 架構

{% asset_img client-server.png "Architecture" %}

Docker 是 client-server 的架構，Docker client 與 Docker daemon 溝通，後者負責構建、運行和分發 Docker 容器的工作。

> [Daemon](https://en.wikipedia.org/wiki/Daemon_(computing)) 是一種在後台執行的電腦程式。

Docker client 和 Docker daemon 可以安裝在同一台電腦中，或是 Docker client 可以連線到遠端的 Docker daemon。他們之間的溝通是使用 Restful API，透過 HTTP 網路或是 UNIX sockets。

> [UNIX socket](https://en.wikipedia.org/wiki/Unix_domain_socket) 用於一台主機的 process 之間溝通，不需要建立在網絡 protocol 之上，主要是基於 file system 而發展的。

## Docker daemon

Docker daemon（`dockerd`）用來接收 API 請求，然後管理各項 Docker 資源，例如：image, container。

## Docker client

Docker client（`docker`）是主要用來跟 Docker 溝通的方法，它會傳送指令到 `dockerd`。

## 結語

像 Docker 這樣子的 client-server 還蠻常見的，通常名稱有 `d` 結尾的，常是代表 daemon 的意思。例如：`sshd`, `systmed`, `supervisord` ... 等。而對應 client 就是 `ssh`、`systemctl`、`supervisorctl`，這邊的 `ctl` 則是 `control` 的意思。
