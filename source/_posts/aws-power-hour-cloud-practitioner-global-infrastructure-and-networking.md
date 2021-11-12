---
title: "AWS Power Hour: Cloud Practitioner | Global Infrastructure and Networking"
date: 2021-11-10 08:30:16
tags:
    - aws
    - cloud practitioner
---

> Building on the previous episode, we’ll explore the global infrastructure of AWS, networking services like the Virtual Private Cloud (VPC) as well as how that infrastructure can be connected to your premises.

<!-- more -->

# 全球基礎設施  <!-- markdownlint-disable MD025 -->

## 資料中心

AWS 的資料中心擁有許多備援機制，即使發生意外斷電了也能夠保證網路連線不會中斷。若這個資料中心發生錯誤，你可以很快的切換到下一個可用區域的資料中心

查看更多關於[資料中心](https://aws.amazon.com/tw/compliance/data-center/controls/)的資訊。

## 區域與可用區域

{% asset_img region-and-ability-zone.png "Region And Ability Zone" %}

可用區域（Ability Zone）由多個資料中心（Data Center）所組成，而可用區域也擁有備援機制。當其中一個可用區域發生錯誤，另一個可用區域會起來取代它，並接續它的工作。而多個可用區域會再組成區域（Region），每個區域之間都有 AWS 專屬的高速、低延遲的網路串連。

假設今天用戶的應用程式建置在 AZ-1A 之中，當 AZ-1A 發生錯誤時，用戶能夠很輕鬆的將他的程式轉移到 AZ-1B，歸功於 AWS 的高速網路。如此一來，應用程式就能保證一定程度的可用性。

AWS 在全球建置了許多區域和可用區域，在[這裡](https://aws.amazon.com/about-aws/global-infrastructure/?nc1=h_ls)可以查看到 AWS 的全球基礎設施。

而區域之間是互相隔離的，這表示 AWS 不會隨意的將用戶資料從一個區域移動到另一個區域，除非得到用戶的允許。

### 區域的選擇

- 管理或監督的需求

  若是有資料安全的疑慮，不希望資料被儲存在其他地區，就可以選擇自己信任的區域。

- 鄰近客戶

  為了降低資料的響應時間，可以選擇鄰近客戶的區域。

- 服務的可用性

  隨著服務的增長，你可能會需要將服務擴展到其他區域，來服務更多的用戶。

- 成本

  依照不同國家或地區的成本，不同的區域會有不同的成本，因此這也會是一個選擇區域的考量點之一。

## CloudFront

Amazon [CloudFront](https://aws.amazon.com/cloudfront) 是一項內容交付網路 ([CDN](https://en.wikipedia.org/wiki/Content_delivery_network)) 服務，專為實現高效能、安全性和開發人員便利性而建置。

{% asset_img without-cdn.png %}

假設今天我們的服務架設在美國，那位在澳洲的用戶利用網路存取服務時，就得經過較長的路徑來存取的資源，例如：圖片、影片 ... 等，這意味著較長的響應時間以及較差的使用者體驗。那我們該如何解決這問題？

{% asset_img cdn.png %}

利用 CloudFront，我們可以決定我們要快取哪些資料。快取就是將資料放在離使用者較近的地方，讓使用者能夠更快速地存取到資料。所以當澳洲的用戶要存取我們的服務時，就不用再大老遠的存取位在美國的資料，只需要存在放在澳洲內的快取即可。

關於快取，有一點要注意的是存活時間（TTL, Time To Live）。設定快取的存活時間，當時效過期時，要重新從原本的資料複製一份過來，避免快取的資料過於老舊。

CDN 對於需要部署在全球的服務來說非常重要，透過 CDN，我們不必在全球 25 個區域中都部署相同的基礎設施，只需要在一個區域內部署，再將資料快取在各個地方即可。

## Outposts

若你需要極度低的延遲，或是有管理的需求需要將資料放置在私有雲，但卻想要享有使用 AWS 服務的好處的話，那 AWS [Outposts](https://aws.amazon.com/outposts/) 或許是一個解決方案。

AWS Outposts 是一個全代管的數據中心，提供同樣的 AWS 基礎架構、AWS 服務、API 和工具。同時，你也可以使用 AWS 區域中的那些不能夠在 Outposts 上執行的服務，實現混合雲的應用。

# 網路

{% asset_img networking.png "Networking" %}

## 虛擬私有雲

Amazon Virtual Private Cloud ([VPC](https://aws.amazon.com/vpc/)) 是一個可以完全控制的虛擬網路環境。

VPC 內可以建立子網域，分別為公有和私有子網路。公有子網域可以被直接的連線，適合放置公開的服務，例如：網頁前端、後端。而私有內無法直連，適合一些需要隱私的服務，例如：資料庫。

公有子網域會透過[網際網路閘道](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)（Internet Gateway）和網際網路之間通訊。而私有子網域則是透過[NAT 裝置](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat.html)（NAT device）連線到網際網路。

[更多關於 VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)。

### 連線方式

- IPsec VPN

使用 VPN 連線至 VPC 可以確保連線是受到加密保護的。AWS 會同時建立兩條網路連線，當其中一條連線發生錯誤，使用者任可以透過另一條通道連線。

{% asset_img vpn.png "VPN" %}

- Direct Connect

Direct Connect 可以減少連線成本、提高網路頻寬。透過 Direct Connect 可以建立 1 Gbps 或 10 Gbps
的網路連線。

{% asset_img dx.png "Direct Connect" %}

[更多連線方式](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/network-to-amazon-vpc-connectivity-options.html)。

## 平衡負載

Elastic Load Balancing (ELB) 會自動將傳入的應用程式流量分配在一個或多個可用區域 (AZ) 中的多個目標和虛擬設備上。

透過平衡負載，當其中一個 AZ 發生錯誤時，可以自動將流量轉移到另外一個 AZ，以提供用戶高可用（High Available）的使用體驗。

[更多關於 ELB](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)。

# 課後問題

1. Each AWS region is composed of two or more locations that offer organizations the ability to operate production systems that are more highly available, fault tolerant, and scalable than would be possible using a single data center. What are these locations called ?
   1. Edge Locations
   2. AWS Local Zones
   3. Available Zones
   4. Compute centers

2. What is the primary benefit of an AWS Edge Location?
   1. Lower costs for content storage
   2. Stronger authentication controls
   3. Data sovereignty controls
   4. Lower latency delivery of content to end users

3. What AWS Cloud service provides a logically isolated areas within the AWS Cloud where organizations can launch AWS resources in a virtual network that the define
   1. Amazon Virtual Private Cloud
   2. Amazon Route 53
   3. Amazon Virtual Private Network
   4. Amazon Direct Connect

答案：

1. `3`
2. `4`
3. `1`
