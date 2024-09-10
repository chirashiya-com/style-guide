# ちらしや WordPressテーマ作成 スタイルガイド

保守・カスタマイズしやすいWordPressサイトを作るためのガイド。  
主な注意点を挙げる。

## 静的ファイルについて

- CSSファイル・画像・JSファイルなどの静的ファイルはワードプレスファイルの外ではなくWordPressのテーマフォルダ内に格納する。
※後述のディレクトリ構成例も参照
- テーマフォルダ内の静的ファイルを読み込む際は、パスの指定にget_template_directory_uri()関数やget_stylesheet_directory_uri()関数（子テーマの場合）を使う。

```
<!-- 【OK】 -->
<img src="<?php echo get_template_directory_uri(); ?>/images/logo.html">

<!-- 【NG】 get_template_directory_uri()関数を使用していない -->
<img src="/wp-content/themes/my-theme/images/logo.html">

<!-- 【NG】 静的ファイルがファイルがテーマフォルダに格納されていない -->
<img src="/images/logo.html">
```

- スタイルシートやJSファイルをテーマファイルに読み込む際は、headに直接記述せず、原則functions.phpに記述して読み込む。

```
<!-- 【NG】header.phpのhead要素内にlinkタグやscriptタグを直接記述 -->
<head>
  <!--略-->
  <link rel="stylesheet" href="<?php echo get_template_directory_uri(); ?>/css/style.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  <script src="<?php echo get_template_directory_uri(); ?>/js/script.js"></script>
  <!--略-->
</head>
```

```
<!-- 【OK】functions.phpにフックを書いてスタイルシートやスクリプトを読み込んでいる -->

// CSS ファイルを読み込み
function add_stylesheet() {
  wp_enqueue_style('reset-handle', get_template_directory_uri() . '/common/css/reset.css', '1.0', false);
  wp_enqueue_style('slick-handle', get_template_directory_uri() . '/slick/slick.css', '1.0', false);
  wp_enqueue_style('slick-theme-handle', get_template_directory_uri() . '/slick/slick-theme.css', '1.0', false);
  wp_enqueue_style('common-handle', get_template_directory_uri() . '/common/css/common.css', '1.0', false);
  wp_enqueue_style('parts-handle', get_template_directory_uri() . '/common/css/parts.css', '1.0', false);
  wp_enqueue_style('top-handle', get_template_directory_uri() . '/common/css/top.css', '1.0', false);
  wp_enqueue_style('page-handle', get_template_directory_uri() . '/common/css/page.css', '1.0', false);

// JSの読み込み
  wp_enqueue_script('jquery-handle', get_template_directory_uri().'/common/js/jquery-3.7.1.min.js');
  wp_enqueue_script('slick-js-handle', get_template_directory_uri().'/common/js/slick.js');
  wp_enqueue_script('slick-min-handle', get_template_directory_uri().'/slick/slick.min.js');
  wp_enqueue_script('config-js-handle', get_template_directory_uri().'/common/js/config.js');
}
add_action('wp_enqueue_scripts', 'add_stylesheet');
```

## Google fontsについて

functions.phpに記述すること。

```
//【OK】
// Google Fonts
function google_font_scripts() {
  wp_enqueue_style( 'google-web-style', '//fonts.googleapis.com/css2?family=Zen+Kaku+Gothic+New:wght@400;500;700;900&display=swap',array(), null );
}

add_action( 'wp_enqueue_scripts', 'google_font_scripts' );
```

## テンプレートファイルの構成について

テーマフォルダのディレクトリ構成例の項も参照。

- 共通部分はheader.php、footer.php、sidebar.phpなどにまとめる。
header.phpには`<!DOCTYPE html>`の記述も含める。
- 必要に応じてテンプレートパーツファイルを作成する。
- headタグ終了直前にはwp_head()関数、bodyタグ開始直後にはwp_body_open()関数、bodyタグ終了直前にはwp_footer()関数への呼び出しを必ず記述する

```
<!-- 【OK】header.php -->
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="format-detection" content="telephone=no,address=no,date=no,email=no">
  <?php wp_head(); ?>
</head>
<body>
<?php wp_body_open(); ?>
<header>
</header>
```

```
<!-- 【OK】footer.php -->
<footer>
</footer>
<?php wp_footer(); ?>
</body>
</html>
```

## 固定ページの作成

管理画面のブロックエディタで作成する固定ページは共通テンプレートのpage.phpを使えばよいが、 HTML/CSSコーディングでつくる必要のある固定ページはpage-{スラッグ名}.phpを作り、HTMLのコーディングはファイルのソースに直書きする。  
※HTMLのソースコードをワードプレスの管理画面の固定ページのブロックエディタや独自のカスタムフィールドから流し込むことは原則しない。

## テーマフォルダのディレクトリ構成例

```
my-theme/
　├─ css/
　├─ images/
　├─ js/
　├─ sass/
　├─ template-parts/
　├─ 404.php
　├─ archive.php
　├─ footer.php
　├─ front-page.php
　├─ functions.php
　├─ header.php
　├─ index.php
　├─ page.php
　├─ page-xxx.php
　├─ page-yyy.php
　├─ page-zzz.php
　├─ single.php
　└─ single-xxx.php
```

## テンプレートファイル内でのワードプレスループ

サブループを回す場合は、原則WP_Queryクラスを使う。query_posts関数などの非推奨関数は使わない。  
WP_Queryに渡すパラーメータは、PHPの配列形式で記述する。

## カスタム投稿タイプ、カスタムタクソノミー

Custom Post Type UIプラグインで作成する。functions.phpの記述で作成しない。

## カスタムフィールド

[Advanced Cumtom Fields](https://ja.wordpress.org/plugins/advanced-custom-fields/)プラグインで作成する。functions.phpの記述で作成しない。

## お問合せフォーム

プラグインを使う場合はContact Form 7かMW WP Formを使用する。  
プラグインを使用しない場合はmail.phpを使う。

## サードパーティ製のテーマをカスタマイズする場合

必ず子テーマを作ってカスタマイズする。親テーマを直接編集しない。


## Googleアナリティクスやタグマネージャーのスクリプトの設置

メンテナンス性が悪くなるので、テンプレートファイルに直接scriptタグを記述するのはできるだけ避ける。  
有料テーマの場合でテーマの設定からhead内にスクリプトを挿入できる場合は、そこから挿入する。

それ以外の場合は、functions.php経由で挿入する。

```
//【OK】functions.php

// Google Tag Manager

function add_gtm_head() {
  echo "<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXXXX');</script>
<!-- End Google Tag Manager -->";
}
add_action('wp_head', 'add_gtm_head', 0);


function add_gtm_body() {
  echo '<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->';
}
add_action('wp_body_open', 'add_gtm_body', 0);
```


## プラグインの導入について

利用したことがないプラグインを導入を検討する場合は以下の点に注意する。

- 最新のWordPressのバージョンと互換性があるか
- 有効インストール数が十分か
- 最終更新が古すぎないか
- そのプラグインを紹介しているブログ記事などを検索し、実際に利用したことのあるユーザーからの評判を確認する
- 稼働中のサイトに未知のプラグインを導入する場合は、本番環境でいきなり導入する前にローカル環境などで動作確認をすることを強く勧める。


### 必須プラグイン

ちらし屋式（仕事のルール）という名称のガイドラインがあるため、そちらの必須プラグインを確認すること。  
また、不要なプラグインは削除すること。

#### Edit Author Slug（著者の記事一覧ページのスラッグを変更）について（必須プラグイン）
- [Edit Author Slug](https://wordpress.org/plugins/edit-author-slug/)

ユーザー → プロフィール → 投稿者スラッグ → カスタム設定に任意のローマ字を入れること。


#### functions.php にも記述すること
- https://www.doe.co.jp/hp-tips/wordpress-login-id-guard/  

```
//【OK】functions.php

//author=id から ユーザ名への転送を避ける
function disable_author_archive_query() {
	if( preg_match('/author=([0-9]*)/i', $_SERVER['QUERY_STRING']) && !preg_match('/post_author=/i', $_SERVER['QUERY_STRING']) ){
		wp_redirect( home_url() );
		exit;
	}
}
add_action('init', 'disable_author_archive_query');

//WP REST API の不要なエンドポイントを削除する
add_filter('rest_endpoints', function ($endpoints) {
	if ( isset( $endpoints['/wp/v2/users'] ) ) {
		unset( $endpoints['/wp/v2/users'] );
	}
	if ( isset( $endpoints['/wp/v2/users/(?P[\d]+)'] ) ) {
		unset( $endpoints['/wp/v2/users/(?P[\d]+)'] );
	}
	return $endpoints;
});

//wp-sitemap.xml 投稿者アーカイブを無効化
function sitemap_hide_user($provider, $name) {
	if ('users' === $name) {
		return false;
	}
	return $provider;
}
add_filter('wp_sitemaps_add_provider', 'sitemap_hide_user', 10, 2);
```


## OGP画像について
[SEO SIMPLE PACK](https://ja.wordpress.org/plugins/seo-simple-pack/) の設定から入れることができるので、そちらから入れることを推奨。  
title、メタディスクリプションを反映するのに、このプラグインを使用するため、一緒にOGPも設定しておく。

## パーマリンク構造について

設定 → パーマリンク → カスタム構造 にて、`/%category%/%post_id%/`を指定することを推奨。  
サイト公開後にこちらのパーマリンクを変更すると、SEOにも悪影響が出ると言われているため、公開後の変更はNG。

## 管理画面ユーザーのメールアドレスについて

デフォルトがwp@のようなアドレスになっているため、納品時までに正式なアドレスを設定すること。

## ローカル環境での開発について

新規のワードプレステーマを作成する場合や既存のワードプレステーマのテンプレートファイルに変更を加える場合は、ローカル環境で確認しながら開発するほうが効率が良い。  
WordPressのローカル環境構築には[Local by Flywheel](https://localwp.com/)を使うのが最も簡単でおすすめ。  
インストール方法や使い方は[こちら](https://lucy.ne.jp/bazubu/local-by-flywheel-33920.html)の記事が参考になる。  
既存のワードプレスサイトのローカルへのコピーにはAll-in-One WP Migrationプラグインを使うと良い。  
使い方は[こちら](https://www.webdesignleaves.com/pr/wp/wp_all_in_one_wp_migration.html)の記事を参照。  

Prefferredの選択で上手くいかない場合は、Apache にすると上手くいくケースがある。  
<img width="800" alt="スクリーンショット 2024-09-10 14 30 57" src="https://github.com/user-attachments/assets/c4fd0dcb-a29e-4ae4-b6f6-e84ebeb0d9e5">
