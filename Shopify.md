# ちらし屋 Shopifyテーマ作成ガイド 2024年作成

- [はじめに](#1はじめに)
- [テーマについて](#2テーマについて)
- [アプリについて](#3アプリについて)
- [支払い方法について](#4支払い方法について)
- [技術参考サイト](#5技術参考サイト)

## 1.はじめに

カナダに本社を置くShopify社が提供する、ECサイトの作成及び運用が可能なサービスである。

海外発のサービスであるため、日本語への対応や日本の商流に対応していないケースがある。  
その場合はテーマのカスタマイズまたは、アプリの導入で補う必要がある。

## 2.テーマについて

- 数多くのテーマがあるが、基本的にテーマに沿った構築と運用を行う。  
- テーマの仕様に沿わないカスタマイズを行うと、保守運用に支障が出る可能性がある。  
- ※テーマに対して直接コードの記述（以下のコードを編集）を行なった場合、テーマのバージョンアップをした際にコードが上書きされる。そのため、テーマのバージョンアップが困難となる。
- 事前に顧客に上記の点を了承いただいた上で、カスタマイズを行うこと。

<img width="1207" alt="スクリーンショット 2024-09-18 13 32 13" src="https://github.com/user-attachments/assets/542d345e-58d6-4353-afea-0b95d383f885">

- 以下のように「テーマ内のカスタムCSS」に記載したコードは消えないため、CSSはこちらに記載する。

<img width="1357" alt="スクリーンショット 2024-09-18 13 31 29" src="https://github.com/user-attachments/assets/4c9a72e2-57d5-4c70-818b-58075dc66b58">

- 以下のように「テーマ内のカスタムLiquid」に記載したコードは消えないため、追加のHTML、Liquidコードはこちらに記載する。

<img width="1417" alt="スクリーンショット 2024-09-18 14 10 51" src="https://github.com/user-attachments/assets/62099382-d82d-4c2a-acba-33b4c63a11ab">


### 無料テーマ

Dawnを推奨する。

### 有料テーマ

ケースに合ったテーマを選定する。  
過去に使用したテーマは管理画面から確認する。

https://dtnavi.tcdigital.jp/shopify/shopify-theme-paid/  
https://ec.huckleberry-inc.com/archives/1482  
https://ja.komoju.com/blog/shopify/shopify-themes/

![スクリーンショット 2024-09-19 10 09 31](https://github.com/user-attachments/assets/587e43f4-ad38-419a-bd2d-12696ed0fcd5)

「Reviews」の欄からテーマのレビューが見れるため、参考になる。

#### ストアのテーマ調査について
- Googleの拡張機能 [Koara](https://chromewebstore.google.com/detail/koala-inspector-shopify-s/hjbfbllnfhppnhjdhhbmjabikmkfekgf?hl=ja) でストアで使用されているテーマやアプリが確認できるため、他のストアの調査に利用できる（見れないストアもある）

## 3.アプリについて

アプリ導入時は、公開されていないテストストアに導入して動作を確認すること。  
アプリを消しても、アプリ自体のコードが残る場合あり、それが不具合に繋がるケースも報告されているため。

#### ▽無料アプリ

・[Shopify Flow（※設定必須）](https://apps.shopify.com/flow?locale=ja)  
リスク「高」の注文は自動キャンセルされるよう設定できます（設定する項目は、過去に構築したストアを見ること）。  
リスク「高」は自動キャンセルしてOKか、アプリ導入時に顧客に確認すること。  

・[配送＆注文サポーター](https://apps.shopify.com/custom-field-app?locale=ja)  
配送日時指定

・[Instafeed](https://apps.shopify.com/instafeed?locale=ja)  
テーマにインスタを反映させる

・[Order Printer](https://apps.shopify.com/shopify-order-printer?locale=ja)  
領収証の発行機能を設定できます。  
アプリ内にLiquidコードを入れる必要があるため、過去に構築したストア（VANGA）から引用することを推奨。

・[Shopifyメール](https://apps.shopify.com/shopify-email)  
会員登録 or メール配信を許可した顧客に対し、メール配信ができるよう設定できる。  


・[商品レビュー](https://apps.shopify.com/judgeme?locale=ja)  
商品注文者のみ、商品のレビューができるよう設定もできる。  
ストア公開前に手動でレビュ―書けるので、載せて欲しいレビューがあれば手動で設定できる。  

・[Search & Discovery](https://apps.shopify.com/search-and-discovery?locale=ja)  
商品の絞り込み検索、関連商品の表示を設定できる。  


#### ▽有料アプリ
・[Ship ＆ Co](https://apps.shopify.com/shipandco?locale=ja)  
送り状発行までのフローを自動化。発行1件につき33円。  

・[MR.DAIBIKI](https://apps.shopify.com/mr-daibiki?locale=ja)  
代引きの金額を、注文管理画面、注文メールに反映できる。  

・[ギフトラッピング＆のし専用アプリ](https://apps.shopify.com/giftwrappingpaper?locale=ja)  
カート画面に「ラッピング、のし」の選択項目を追加できる。  

・[Hextom: Translate and Currency](https://apps.shopify.com/translate-my-store?locale=ja)  
ストアの多言語化

## 4.支払い方法について

### 支払いの種類

事前に各サービスと連携が必要な決済があるため、導入前に確認すること。

- Amazon Pay、PayPal、コンビニ決済（KOMOJU）、Diners Club、LINE Pay、PayPay、メルPay。

Shopifyペイメントを有効にした場合の決済。

- Visa、Mastercard、アメリカンエキスプレス、JCB（審査に最大3週間程掛かる場合あり）、Shop Pay、Apple Pay、Google Pay

### メールの文面

支払い方法（銀行振込、代引き、郵便振替）に応じて、注文メールのカスタマイズが必要になる。  
必ず各支払い毎にテスト注文を行い、届くメールの内容を確認すること。  
https://help.shopify.com/ja/manual/checkout-settings/test-orders  
https://help.shopify.com/ja/manual/payments/shopify-payments/testing-shopify-payments

## 5.技術参考サイト

- [Shopify公式 dev(Tags)](https://shopify.dev/docs/api/liquid/tags#liquid)
- [Shopify公式 dev(Object)](https://shopify.dev/docs/api/liquid/objects)
- [Shopify公式 技術的なQ&A](https://community.shopify.com/c/%E6%8A%80%E8%A1%93%E7%9A%84%E3%81%AAq-a/bd-p/tqa-jp)
- [Liquidチートシート](https://www.shopify.com/partners/shopify-cheat-sheet)
- [しょぴくら](https://crafti-fy.jp/blogs/shopify)  
- [ハックルベリー(Shopifyアプリ開発大手)](https://ec.huckleberry-inc.com/)  
- [ハックルベリー(Shopify最速アップデート情報)](https://www.youtube.com/@Huckleberry-shopify/videos)
