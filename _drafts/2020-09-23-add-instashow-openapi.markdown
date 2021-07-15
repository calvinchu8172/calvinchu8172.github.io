---
layout: post
title:  "Implement InstaShow OpenAPI"
date:   2020-09-22 20:13:07 +0800
categories: webrtc
---

## InstaShow Object Storage API

### InstaShow Object Storage API 是什麼服務？最主要的用途是什麼？

* Object Storage 是用來提供所有串接 InstaShow 的硬體裝置（Device）或行動應用程式（Mobile APP or Web APP）存取 InstaShow User 資料的服務。

### 設想可能應用的情景，例如：

* 某個 Mobile APP 需要登入某個身份管理 Server 以取得 InstaShow User 的資料存取授權。
* InstaShow User 可登入身份管理 Server 管理 Mobile 或 Device 的存取授權。
* 某個 Device 會列出 InstaShow User 所有的 Mobile APP。
* 某個 Device 或 Mobile APP 會存取 InstaShow User 的圖片、影片或其他檔案。

### Device 或 APP 可以存取的資料範圍為何？

* 所有的 Mobile App 在透過 SSO Server 取得 InstaShow User 的 **Access Token** 後，只能存取該 InstaShow User 下對應的 Mobile APP 內所有的資料。

### Device 或 APP 要怎麼使用 Object Storage？

* Mobile App 透過 SSO Server 取得 InstaShow User 的 **Access Token** 後，參數帶上 **Access Token** 驗證，可使用 **RESTful API** 提交存取：

### Object Storage Work Flow

* 流程為 User -> Mobile or Web Application -> SSO Server -> Get Access Token -> Application Domain -> Object Key -> Content 。

![Work Flow](/assets/open-api/work-flow.png)

### Object Storage Structure

![Structure](/assets/open-api/lambda-structure.png)

架構中每個項目的用途為：

1. Administrator 需要在 SSO Server 後台建立 Application，使 Application 得以登入 SSO Server。
2. InstaShow User 使用 Application 在 SSO 註冊或登入，取得 Access Token。
3. 取得 Access token 後，Access Token 只會對應一個 Application，所以 Lambda 的 API 路由不需要有 `/application/`，參數帶 Access Token，Lambda 會去搜尋對應的 Application。
4. Application 旗下可能會有多個 Application Domain，代表所屬的功能。
5. Application Domain 旗下可能會有多個 Object Key，代表存取某個資源（Resource）的連結，例如 S3 裡的檔案，或 DynamoDB 某個 Table 的欄位裡的 json 格式資料。


### API 路由規劃

#### EC2 SSO Server 部分（路由加上 v1 為版本）

* 列出 User 所有 Application
  * `GET v1/applications`
* 列出 User 特定 Application 的詳細資料
  * `GET v1/applications/(application_name)`
  * EX: `GET v1/applications/picture_sharing_app`
* 建立、修改、刪除 User 的 Application 不提供 API，因為只有 Administrator 才有權限


#### Lambda Object Storage 部分

* 列出所有 Application Domain
  * `GET v1/domains`
* 列出特定 Application 的詳細資料
  * `GET v1/domains/(domain_name)`
* 建立新的 Application Domain
  * `POST v1/domains`
* 修改 Application Domain
  * `PUT v1/domains/(domain_name)`
* 刪除 Application Domain
  * `DELETE v1/domains/(domain_name)`
* 列出特定 Application Domain 所屬所有的 Object Key
  * `GET v1/domains/(domain_name)/objects`
* 列出特定 Application Domain 所屬特定的 Object 的 Object Key 的詳細資料
  * `GET v1/domains/(domain_name)/objects/(object_key)`
* 建立新的 Object Key
  * `POST v1/domains/(domain_name)/objects`
* 修改特定 Object Key 的資料
  * `PUT v1/domains/(domain_name)/objects/(object_key)`
* 刪除特定的 Object Key
  * `DELETE v1/domains/(domain_name)/objects/(object_key)`


## 資料庫規劃

* SSO Server Database 使用關連式資料庫 MySQL
  * User (MySQL user table, name, email 等...欄位)
  * Application (MySQL application table，要有 user_id, name 等...欄位)
  * Access Token (MySQL access_token table，要有 application_id, token 等...欄位)
* Object Storage Database 使用 NoSQL DynamoDB
  * Domain (DynamoDB，要有 applicaiton_id，domain_name 等...欄位)
  * Object Key (DynamoDB，要有 Domain_id，object_key 等...欄位)









