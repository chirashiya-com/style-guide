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
# 【OK】functions.phpにフックを書いてスタイルシートやスクリプトを読み込んでいる
add_action('wp_enqueue_scripts', 'my_wp_enqueue_scripts');
function my_wp_enqueue_scripts() {
  wp_enqueue_style( 'common-style', get_template_directory_uri() . '/style.css' );
  wp_enqueue_script( 'jquery' ); #WP内蔵のjQueryを使用
  wp_enqueue_script('common-script', get_stylesheet_directory_uri(). '/js/script.js', array('jquery'));
}
```

## テンプレートファイルの構成について

テーマフォルダのディレクトリ構成例の項も参照。

- 共通部分はheader.php、footer.php、sidebar.phpなどにまとめる。
header.phpには`<!DOCTYPE html>`の記述も含める。
- 必要に応じてテンプレートパーツファイルを作成する。
- headタグ終了直前にはwp_head()関数、bodyタグ開始直後にはwp_body_open()関数、bodyタグ終了直前にはwp_footer()関数への呼び出しを必ず記述する
