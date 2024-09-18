# ちらし屋 Shopifyテーマ作成ガイド 2024年作成

- [はじめに](#1はじめに)
- [テーマについて](#2テーマについて)
- [アプリについて](#3アプリについて)

## 1.はじめに

カナダに本社を置くShopify社が提供する、ECサイトの作成及び運用が可能なサービスである。

海外発のサービスであるため、日本語への対応や日本の商流に対応していないケースがある。  
その場合はテーマのカスタマイズまたは、アプリの導入で補う必要がある。

## 2.テーマについて

- 数多くのテーマがあるが、基本的にテーマに沿った構築と運用を行う。  
- テーマの仕様に沿わないカスタマイズを行うと、保守運用に支障が出る可能性がある。  
- ※テーマに対して直接コードの記述（以下のコードを編集）を行なった場合、テーマのバージョンアップをした際にコードが上書きされる。そのため、テーマのバージョンアップが困難となる。

<img width="1207" alt="スクリーンショット 2024-09-18 13 32 13" src="https://github.com/user-attachments/assets/542d345e-58d6-4353-afea-0b95d383f885">

- 以下のように「テーマ内のカスタムCSS」に記載したコードは消えないため、CSSはこちらに記載する。

<img width="1357" alt="スクリーンショット 2024-09-18 13 31 29" src="https://github.com/user-attachments/assets/4c9a72e2-57d5-4c70-818b-58075dc66b58">


### 無料テーマ

Dawnを推奨する。

### 有料テーマ

ケースに合ったテーマを選定する。

https://dtnavi.tcdigital.jp/shopify/shopify-theme-paid/  
https://ec.huckleberry-inc.com/archives/1482  
https://ja.komoju.com/blog/shopify/shopify-themes/

## 3.アプリについて

アプリ導入時は、公開されていないテストストアに導入してみて動作を確認すること。  
アプリを消しても、アプリ自体のコードが残る場合あり、それが不具合に繋がるケースも報告されているため。

#### ▽無料アプリ

・Shopify Flow（※設定必須）  
リスク「高」の注文は自動キャンセルされるよう設定できます（設定する項目は、過去に構築したストアを見ること）。  
リスク「高」は自動キャンセルしてOKか、アプリ導入時に顧客に確認すること。  
https://apps.shopify.com/flow?locale=ja

・配送＆注文サポーター（配送日時指定）  
https://apps.shopify.com/custom-field-app?locale=ja

・Instafeed（TOPページににインスタを反映させるのか）  
https://apps.shopify.com/instafeed?locale=ja

・Order Printer
領収証の発行機能を設定できます。  
https://apps.shopify.com/shopify-order-printer?locale=ja

・Shopifyメール  
会員登録 or メール配信を許可した顧客に対し、メール配信ができるよう設定できます。  
https://apps.shopify.com/shopify-email

・商品レビュー  
商品注文者のみ、商品のレビューができるよう設定もできます。  
ストア公開前に手動でレビュ―書けるので、載せて欲しいレビューがあれば手動で設定できます。  
https://apps.shopify.com/judgeme?locale=ja

・Search & Discovery  
商品の絞り込み検索、関連商品の表示を設定できます。  
https://apps.shopify.com/search-and-discovery?locale=ja


#### ▽有料アプリ
・Ship ＆ Co  
送り状発行までのフローを自動化。発行1件につき33円。  
https://apps.shopify.com/shipandco?locale=ja

・MR.DAIBIKI  
代引きの金額を、注文管理画面、注文メールに反映できます。  
https://apps.shopify.com/mr-daibiki?locale=ja

・ギフトラッピング＆のし専用アプリ  
カート画面に「ラッピング、のし」の選択項目を追加できます。  
https://apps.shopify.com/giftwrappingpaper?locale=ja

・Hextom: Translate and Currency（ストアの多言語化）  
https://apps.shopify.com/translate-my-store?locale=ja

