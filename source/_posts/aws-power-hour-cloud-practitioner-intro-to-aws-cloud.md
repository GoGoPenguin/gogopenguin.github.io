---
title: "AWS Power Hour: Cloud Practitioner | Intro to AWS Cloud"
date: 2021-11-08 09:04:11
tags:
    - aws
    - cloud practitioner
---

> Learn about the six benefits of cloud, common cloud adoption strategies, and cloud compute. We’ll explore compute services by digging into Amazon Elastic Compute Cloud (Amazon EC2) with a focus on helping you understand the important aspects of creating an EC2 instance.

<!-- more -->

# AWS 證照 <!-- markdownlint-disable MD025 -->

下圖為 AWS 可用的證照：

左邊灰底為「角色型認證」的證照，依照工作職稱或是需求的不同，可以選擇相關的證照。

右邊則是指定專業領域的「專家級」證照。

![Available AWS Certifications](https://miro.medium.com/max/1400/1*4fl-1Eh_yI1cVPYaROn_3w.png)

相關網址：

- [AWS 證照](https://www.google.com/aclk?sa=L&ai=DChcSEwim_MzJ_4n0AhULupYKHS3yCLIYABAAGgJ0bA&ae=2&sig=AOD64_3qeem0qBNX0ACU1IaetgUfWbonzQ&q&adurl&ved=2ahUKEwjsqcbJ_4n0AhWbdd4KHWZsCDoQ0Qx6BAgDEAE)
- [按角色或解決方案進行學習](https://aws.amazon.com/training/learn-about/)

# 關於考試

- Q: 題數
  - A: 65
- Q: 種類
  - A: 多選題、複選題
- Q: 時間
  - 90 分鐘
- Q: 費用
  - A: 100 美金
- Q: 總分
  - A: 最低 100 分，滿分 1000 分，700 分及格
- Q: 考場
  - A: 集中考場或線上考試，但需要有 Webcam
- Q: 如何安排考試
  - A: 到[這裡](https://www.aws.training/certification)報名

# 什麼是雲？

「雲」是一種透過網路按需求的 IT 資源，採用多少算多少的付費模式。
> Cloud computing is the on-demand delivery of IT resources via the internet with a pay-as-you-go pricing model

那「IT 資源」又是什麼？它包含：

- 計算資源（Compute）
- 資料庫（Database）
- 儲存空間（Storage）

雲的好處是你可以隨時透過網路去租借資源，且隨時都能夠終止。

# 部署方式

{% asset_img deployment-models.png "Deployment Models" %}

- 私有雲（on-premises）
- 公有雲 (cloud deployment)
- 混合雲（hybrid deployment）

# 使用雲端的好處

- 節省費用支出

  使用雲端服務可以減少前期開發時的硬體成本，因為雲服務可以依據使用量來計價，不必一次購入昂貴的機器。

- 不用自己維護機器

  將維護的工作交給雲端公司，讓開發人員能夠更專注於開發應用程式上面。

- 不用猜測要多大機器規格

  雲端主機能依據使用量來[自動擴展](https://en.wikipedia.org/wiki/Autoscaling)（auto-scaling），在滿足需求的同時又能夠省去不必要的花費

- 受益於巨大的規模經濟

  雲端服務公司擁有數以萬計的使用者，讓他們在購買硬體設備時，能夠以更低的價額購入，最後再以便宜的租借成本回饋給使用者。

- 增加速度以及敏捷

  今天我有個點子，只需要用滑鼠點擊就能夠租借到運算資源，不花時間去準備硬體設備。若這點子成功，那就太棒了；若是失敗，也可以簡單地關閉服務，而且我只需要負擔我所使用的部分。

- 將服務部署到全世界

  AWS 在全球都有部署機器，所以我們能夠很簡單的將應用程式部署到世界各地。

# 三種使用 AWS 的方式

- AWS 管理主控台

  這是最簡單也是最直覺的方式。

  ![AWS Management Console](https://d1.awsstatic.com/AWS-Management-Console/Polaris%20Console%20Home.6f773790a19ed7c9a37fcfeddb09076cc52a44e8.png)

- [CLI](https://aws.amazon.com/cli/?nc1=h_ls)（Command Line Interface）

  若是想要在自動化之中去驗證或是存取 AWS，那就能夠使用這方法。

- SDK（Software Development Kit）

  舉凡 `Python`、`.NET`、`JAVA`、`NodeJS` ... 等等，都有相對應的套件能夠去使用 AWS 的資源。

# Amazon Elastic Compute Cloud (Amazon EC2)

EC2 使用虛擬化技術，輕鬆地在一台實體主機上面運行多個 EC2 服務。他們可以實行不同的作業系統，例如：Windows, Linux 甚至 Mac OS。

不必擔心 EC2 之間會去互相干擾影響，因為他們是使用 [Hypervisor](https://zh.wikipedia.org/wiki/Hypervisor) 技術去做管理，虛擬機始終受到保護且彼此獨立。

> 補充：這邊的「虛擬機」是指 [VMware](https://www.vmware.com/tw.html) 或是 [VirtualBox](https://www.virtualbox.org/) 這類型的產品。而[OpenStack](https://www.openstack.org/) 為一種開源雲端軟體，用來管理機器上虛擬機。

讓我們回想一下，若是使用自架機器的方案，當今天使用量增加，你能夠去購買更多台設備來應付突如其來的大量請求，但這不是立即的。使用 EC2 的話，只需要在網頁上點幾下，只需要幾分鐘內就能夠擴展到符合需求的硬體規格。甚至可以設定自動擴展，如此一來就不需要人工介入。

## 啟動一台 EC2

- 到 AWS 管理主控台搜尋 EC2

- 點選右上角「啟動實例」

- 選擇 AMI（Amazon Machine Image）

  AMI 可以視為 EC2 的模板，它可能是一個基本的作業系統，或是由第三方開發商提供的應用程式。

  可以從左邊選單，去選擇不同類型的 AMI

  - Quick Start

    這裡包含了一些基本的 AMI，包含：`Ubuntu`、`Windows`、`REHL`、`Mac OS` 等。

  - AWS Marketplace

    這裏則是由第三方開發商提供的，內建一些他們所提供的應用程式，例如：`OpenVPN`、`LAMP` 等。

  - My AMIs

    你也可以自己建立屬於自己的 AMI，然後在未來重複使用，或是分享給其他人。

- [選擇機器種類](https://aws.amazon.com/tw/ec2/instance-types/)

  EC2 有許多不同類型可以選擇，依照不同需求來選擇不同類型的機器。

  {% asset_img instance-type.png "Instance Type" %}

  以 `t3.medium` 為例：

  - `t` 代表一般用途
  - `3` 代表世代，AWS 定期發佈新一代的機器，通常新的世代會擁有更好的性價比
  - `medium` 代表機器大小，擁有更多的 CPU 核心和記憶體

- 詳細設定

  這邊先介紹其中幾項設定：

  - Number of instances

    你可以設定一次要啟動起個 EC2 實例。

  - Network

    指定 EC2 要在哪個虛擬網路下執行。

  - User data

    使用者可以在這邊填入腳本，當 EC2 啟動後會去執行它。

- 設定容量

  你可以去設定 EC2 的硬碟容量

- 設定標籤

  新增標籤可以幫助分類管理 EC2

- 設定「安全群組」

  安全群組（Security Group）可以當作一種防火牆，它用來設定網路規則

- 選擇金鑰

  [金鑰](https://en.wikipedia.org/wiki/Public-key_cryptography)分別為公鑰和私鑰，來於之後要 ssh 到 EC2 時使用。

# 課後問題

1. Which of the following is an advantage of cloud computing? (Select Two)
   1. Help you more easily reach your custom around your city
   2. Eliminates having to guess your infrastructure capacity needs
   3. Ensure you meet all your security compliance requirements
   4. Increase speed to market
   5. Reduce the need for developers to write code

2. What are the benefits of using Amazon EC2 instances compared to physical on-premises servers? (Select Two)
   1. The flexibility to scale capacity on demand
   2. The short delivery time when you order an Amazon EC2 instance
   3. The ability to attach your own physical disks on Amazon EC2 instance hardware
   4. You can permanently run enough instances to handle peak workloads
   5. You only pay for the capacity the you provision

答案：

1. `2` 和 `4`

2. `1` 和 `5`

這裡還有 30 題的[線上測驗](https://amazonmr.au1.qualtrics.com/jfe/form/SV_eyBlfVF4Sloz1zL?CPEPowerHour=APR21IntroAWSCloud)
