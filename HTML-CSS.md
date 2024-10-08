# ちらし屋HTML/CSSスタイルガイド 2024年作成

- [はじめに](#1はじめに)
- [基本方針](#2基本方針)
- [HTML/CSS基本ルール](#3htmlcss基本ルール)
  - [目的に応じたマークアップ](#目的に応じたマークアップセマンティックなマークアップをする)
  - [インデント](#構造がひと目でわかるようにインデントをつけるインデントはスペース２つにする)
  - [空要素の末尾](#空要素の末尾)
  - [パス表記](#パス表記)
  - [クラス名やid名の命名](#クラス名やid名の命名について)
  - [画像の取り扱い](#画像の取り扱いについて)
  - [mp4動画](#mp4動画について)
  - [サイトの企業ロゴ](#サイトの企業ロゴについて)
  - [target_blank属性](#a要素にtarget_blank属性を付ける場合はrelnoopener-noreferrer属性もつける)
  - [htmlを一通り書く](#htmlを一通り書いてからcssを書く任意)
- [CSSのスタイルガイド](#4cssのスタイルガイド)
  - [cssの基本フォーマット](#cssの基本フォーマット)
  - [不要なスタイルの重複記述を避ける](#不要なスタイルの重複記述を避ける)
  - [スタイルは原則クラスに当てる](#スタイルは原則クラスに当てる)
  - [クラスの命名には一貫した命名規則を採用](#クラスの命名には一貫した命名規則を採用する)
  - [要素セレクタを併記しない](#要素セレクタを併記しない)
  - [要素セレクタ単体にスタイルを当てない](#要素セレクタ単体にスタイルを当てない)
  - [idセレクタに直接スタイルを当てない](#idセレクタに直接スタイルを当てない)
  - [idセレクタ経由でスタイルを当てる場合](#idセレクタ経由でスタイルを当てる場合)
  - [セレクタのネスト入れ子](#セレクタのネスト入れ子はほどほどに)
  - [モジュールごとにスタイルをつける](#モジュールごとにスタイルをつける)
  - [インラインスタイルは原則使用しない](#インラインスタイルは原則使用しない)
  - [単位に関する注意事項](#単位に関する注意事項)
  - [リセットcss](#リセットcssを使用する)
  - [sassについて](#sassについて)
  - [レスポンシブ対応](#レスポンシブ対応について)
  - [ブラウザサイズ](#ブラウザサイズについて)
  - [インナー幅](#インナー幅について)
  - [余白の方向](#余白の方向について)
  - [width、heightの固定値](#widthheightの固定値について)
  - [ボタン](#ボタンについて)
  - [ogp、ファビコン、ウェブクリップ画像](#ogp画像ファビコンウェブクリップ画像について)
  - [title、meta属性について](#titlemeta属性について)
  - [CSSフレームワーク](#CSSフレームワーク)

## 1.はじめに

HTML/CSSのコーディングは自由度が高いため、コーダーが独自のルールで書くと修正や拡張がしにくいコードが作られがちです。  
そのような事態を回避するには、一貫した規則や設計のもとにコードを書くことが重要です。  
一貫したルールや設計のもとでコードを書くことにより以下のような効果が期待できます。

- コードの品質を一定以上にたもつことができる。
- 保守や修正にかかる労力を削減することができる。
- コードを書く際の迷いが減るため開発スピードが向上する。

本ドキュメントでは、メンテナンス性が高いコードを書くために重要だと思われるポイントをスタイルガイドとしてまとめました。
なお、本スタイルガイドは以下のドキュメントや記事を参考に作成しています。

[Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)


## 2.基本方針

### メンテナンス性の高いコードを書く

- 一度書いたら終わりではなく、継続的に保守されることを前提にコードを書く。
- 自分以外の第三者が見ても理解できるコードを書くこと意識する。


### ローカルルールも尊重する

- もし既存のコードに修正や追加をする場合は、まずコードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務める。
- もし一貫したルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く方が良い。

## 3.HTML/CSS基本ルール

### 目的に応じたマークアップ(セマンティックなマークアップ)をする

- HTML要素は目的に応じたものを選んで使う。例えば見出しはh1～h6要素、段落にはp要素を使う、など。

```
<!-- 【OK】 -->
<section>
<h2>ガイドライン</h2>
<p>テキスト<a href="/test/index.html">リンクのテキスト</a></p>
</section>
```

- h1タグは1ページに1つのみで、重複している際は必ず修正する。
- よくあるケースがWordPressにて、ロゴのh1タグとサブページ見出しのh1が被っていることがあるので注意。

```
<!-- NG -->
<header>
  <h1>
    <img src="image/common/logo.svg" alt="株式会社〇〇">
  </h1>
</header>
<main>
  <section>
    <h1>見出し</h1>
  </section>
</main>
```

- その場合は、「TOPページのロゴはh1」「サブページのロゴはdivタグ」に変更し、サブページの見出しをh1とすること。

```
<!-- 【OK】TOPページ -->
<header>
  <h1>
    <img src="images/common/logo.svg" alt="株式会社〇〇">
  </h1>
</header>
<main>
  <section>
    <div>TOPページ見出し</div>
  </section>
</main>
```

```
<!-- 【OK】サブページ -->
<header>
  <div>
    <img src="images/common/logo.svg" alt="株式会社〇〇">
  </div>
</header>
<main>
  <section>
    <h1>サブページ見出し</h1>
  </section>
</main>
```
  

### 構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする</h3>

- コードを見て論理構造がわかるようにインデントをつける。
- ネストが深くなると読みにくくなるため、インデントはスペース２つを推奨する。<br>※Visual Studio Codeなどのテキストエディタではネストの種類(スペースorタブ)や大きさ(何個分)か変更できる。


```
<!--【OK】スペース2つでインデントがつけられている -->
<dl class="form-item">
  <dt class="form-item__title">名前</dt>
  <dd class="form-item__desc">
　  <input class="form-item__input text-field" type="text" name="name">
  </dd>
</dl>
```

```
/* OK(スペース2つでインデントがつけられている) */
@meida screen and (max-width: 767px) {
  .logo {
    font-size: 24px;
  }
}
```

### 空要素の末尾

空要素は末尾スラッシュ文字なし（HTML構文）で記述する。

```
<-- 【OK】 -->
<br>
<img src="/images/top/test.jpg" alt="">
```

```
<!-- 【NG】 -->
<br />
<img src="/images/top/test.jpg" alt="" />
```

### パス表記

サイト内のリソースへのパス表記は、基本的にルートパス（/から始まる表記）で記述すること。

```
<!-- 【OK】 -->
<img src="/subpage/example.png" alt="">
```

```
<!-- 【非推奨】 -->
<!-- 相対パスになっている -->
<img src="test.png" alt="">
<img src="./test.png" alt="">

<!-- 絶対パスになっている -->
<img src="https://example.com/test.png" alt="">
```


### クラス名やID名の命名について
#### 単語の区切りには-(ハイフン)を使う

id名やクラス名に複数単語からなる語を当てる場合、記法単語の区切りは原則ハイフンを用いる。

```
<!--【OK】ハイフンつなぎ(ケバブケース) 
HTMLで最も一般的な記法　-->
<h1 class="top-level-heading">ちらし屋ドットコム</h1>
```

```
<!--【一応OK】大文字つなぎ(キャメルケース)
こちらもNGではないが、原則ケバブケースを優先する。 -->
<h1 class="topLevelHeading">ちらし屋ドットコム</h1>
```

```
<!--　【NG】アンダースコアつなぎ(スネークケース)
PHPやRubyの変数名などの命名にはよく使われる記法だが、HTMLでこの記法を用いるのは推奨しない。 -->
<h1 class="top_level_heading">ちらし屋ドットコム</h1>
```

#### 目的に応じたわかりやすい名前をつける
ハンバーガーボタンのクラス / IDのネーミング例

```
<!-- 【OK】長くてもわかりやすさ優先 -->
<button class="hamburger-button" id="hamburger-button"></button>
```

```
<!-- 【OK】略語でもすぐに意味がわかるものはOK -->
<button class="ham-button" id="ham-button"></button>
```

```
<!-- 【NG】hbが何を意味するのかわかりづらい -->
<button class="hb" id="hb"></button>
```

```
<!-- 【NG】button1がハンバーガーボタンだとわからない -->
<button class="button1" id="button1"></button>
```

#### ローマ字での命名はしない

- <b>OK</b>　heading image
- <b>NG</b>　midashi gazou

### 画像の取り扱いについて

<ul>
  <li>画像を使わずともCSSで再現できそうなものはできるだけCSSで再現するようにする。一般的にはCSSのほうがきれいに表示され、読み込み速度も速い。</li>
  <li>文字は原則として画像を利用すべきではなく、HTMLのテキストとして打ち込むべきである。<br>ただし、デザインで指定されているフォントが有料フォントの場合で、テキストの内容が変更される可能性が低い箇所については、テキストを画像として配置しても良い。その場合、以下の点に注意する。
    <ul>
      <li>alt属性にテキストの内容を必ず打ち込む</li>
    </ul>
  </li>
  <li>画像のサイズ・形式について
    <ul>
      <li>写真はJEPG形式を用いる。ファイルサイズが大きい場合は圧縮する。大きめの画像でも200MB以下になるのが望ましい。</li>
      <li>アイコンやテキスト画像は、SVG形式で書き出せる場合はSVG形式を使うのが望ましい。SVGで書き出せない場合はPNG形式を利用する。</li>
      <li>ビットマップ形式で画像を書き出す場合に、高解像度ディスプレイに対応するためにできれば2xの解像度で書き出すのが望ましい。</li>
    </ul>
  </li>
</ul>

[jpg、pngの使い分けについて](https://github.com/chirashiya-com/style-guide/blob/main/IMAGE.md)

#### img要素にはalt属性を必ずつける

※altに入れるテキストが不明な場合は、納品までに必ず確認して入れること。altが空のまま納品しない。

```
<!--【OK】-->
<img src="./images/sample.png" alt="サンプル画像">
```

```
<!--【OK】画像に関する説明が不要であれば、alt属性の値は空でもOK(※alt属性自体の省略はNG) -->
<img src="./images/foo.png" alt="">
```

#### img要素にはwidth属性とheight属性を必ず記述する

- ページの読み込み速度に有利と言われている。<br>また、SVG形式の画像や、2xの解像度で書き出した画像のデフォルトの大きさを設定するのに使うと便利。
- width、height属性の記述がない場合、ブラウザが画像サイズを再計算する動作が生じるため、読み込み速度に影響が出ると言われている。
- [レイアウトシフトの防止になるため](https://coliss.com/articles/build-websites/operation/work/avoiding-img-layout-shifts.html)


```
<!--【OK】width、heightの両方必須 -->
<img src="./images/sample.png" alt="サンプル画像" width="120" height="60">
```


#### ブラウザに最初に表示される領域以外は、loading="lazy"を必ず記述する

```
<!--【OK】loading="lazy" -->
<img src="./images/sample.png" alt="サンプル画像" width="120" height="60" loading="lazy">
```

#### 画像ファイルの命名
役割が分かるように接頭辞を入れることを推奨する。<br>ファイル内に並ぶ画像もabc順になるため、画像の管理がしやすくなる。

接頭辞の例

- ico- アイコン（例 ico-star.png）
- pic- 写真 または img- 写真
- txt- テキスト
- bg- 　背景
- arw- 矢印<br>など


### mp4動画について

20MB以下に抑えるように圧縮することを推奨。
(mp4動画は、PC、スマホが省電力モードの時は再生されない）


### サイトの企業ロゴについて

極力SVG画像を使用すること。  
（標準ではWordPressのメディアにSVGは入れられないため、オリジナルサイト作成時はSVGを極力入れる）

### a要素にtarget="_blank"属性を付ける場合は、rel="noopener noreferrer"属性もつける

XSS攻撃に対する脆弱性を防ぐため。

```
<!--【OK】-->
<a href="https://www.example.com/" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
```

```
<!--【NG】-->
<a href="https://www.example.com/" target="_blank">新しいタブで開く</a>
```

### HTMLを一通り書いてからCSSを書く（任意）

HTMLとCSSは同時に書くのは避ける。HTMLとCSSを並行して書くと、設計にブレが生じやすく、コーディングスピードも遅くなる。<br>
HTMLを書き終わってからCSSを書くほうが、設計に一貫性をもたせやすく、コーディング完了までのスピードも速くなる。


## 4.CSSのスタイルガイド

GoogleのエンジニアPhilip Waltonによる記事「[CSS Architecture](https://philipwalton.com/articles/css-architecture/)」では、CSSを設計する時に目指すべき４つのゴールが紹介されている。

- 予測しやすい - クラス名や構造などからふるまいを容易に想像できる。
- 再利用しやすい - 必要に応じて他の場所でも同じように使いまわしができる。
- 保守しやすい - 新たな要素を追加したり、既存の要素を修正したりしたりした時に、他の要素を壊すことがない。
- 拡張しやすい - 誰かがCSSを後に編集することになっても、容易に編集できる。
  
このCSSスタイルガイドもこれらのゴールを満たすCSSを書くことを目指している。

### CSSの基本フォーマット

以下のフォーマットに従って書く。

```
/* セレクター名(.selector)と{の間はスペースを一つ空ける */
/* プロパティ名(font-size)の後ろのコロン(:)と値(16px)の間はスペース１つ空ける */
/* 複数セレクタを指定する場合は改行をする */
/* 閉じカッコは新しい行に入れる */
.selector { 　　
  font-size: 16px;
  letter-spacing: 0.1em;
}
/* 新たなセレクタを書くときは１行空ける */
.selector-foo,
.selector-bar,
.selector-baz {　
  margin: 0; 
  padding: 0;
}
```

#### 適宜コメントを入れる

スタイルが何のためのものなのかわかるようにCSSファイルに適宜コメントを書くようにする。

- コメントの例

```
/* スタイルのリセット */
img {
  vertical-align: top;
  max-width: 100%;
}

/* インナー幅 */
.inner {
 max-width: 1200px;
 width: 100%;
 margin-inline: auto;
}
```

### 不要なスタイルの重複記述を避ける

不要な重複記述は保守性を悪化させるため、不必要なスタイルの記述の重複がないようする。

```
/*【NG】無駄な重複がある。 */
.text {
  margin-bottom: 20px;
  color: #333;
  font-size: 24px;
  line-height: 1.6;
  letter-spacing: 0.01em;
}

@media screen and (max-width: 767px) {
  .text {
    margin-bottom: 14px; 
    color: #333; /* ※重複 */
    font-size: 20px; 
    line-height: 1.6; /* ※重複 */
    letter-spacing: 0.01em; /* ※重複 */
  }
}
```

```
/* 【OK】不要な重複がない */ 
.text {
  color: #333;
  font-size: 24px;
  line-height: 1.6;
  letter-spacing: 0.01em;
  margin-bottom: 20px;
}

@media screen and (max-width: 767px) {
  .text {
    font-size: 20px;
    margin-bottom: 14px; 
  }
}
```

### スタイルは原則クラスに当てる

スタイルは原則としてクラスに記述する。 スタイルをクラスに当てることは以下のようなメリットがある。

- スタイルの影響範囲を限定できる
- スタイルの再利用がしやすい
- スタイルの詳細度をある程度一定に保つことができるので、上書きや変更がしやすい。

idセレクタや要素セレクタにスタイルを当てることのデメリットについては後述する。

```
/* 【OK】クラスセレクタにスタイルを当てている */
.top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

### クラスの命名には一貫した命名規則を採用する

- メンテナンス性の高いCSSを書くには、クラスの命名に一貫したルールをもたせるのが非常に重要である。
- クラスの命名規則に特に指定はないが、必ず命名に一貫したルールをもたせること。
- 代表的な命名規則を挙げるが、導入前は社内で確認をすること。（BEM、OOCSS、SMACSS、FLOCSS）

### 要素セレクタを併記しない

スタイルが要素名に依存してしまうのでNG。  
例えば以下の例だと、HTML側でh1をpに変更した場合、スタイルが効かなくなってしまうので、メンテナンス性が悪い。

```
/* 【NG】要素セレクタを併記している */
h1.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

### 要素セレクタ単体にスタイルを当てない
要素セレクタ単体にスタイルを当てると、影響範囲が広すぎるため意図しないところでのスタイルが崩れる可能性がある。  
要素セレクタ単体にスタイルを当てるのは、スタイルをリセットするときのみにする。

```
/* 【NG】スタイルを要素セレクタに直接設定している */
h1 {
  padding: 10px 0;
  font-size: 20px;
  color: #333;
  letter-spacing: 0.04em;
  text-align: center;
}
```
▽要素セレクタにリセット用のスタイルを設定するのはOK

```
/* 【OK】スタイルのリセット */
img {
  vertical-align: top;
  max-width: 100%;
}

ul {
  list-style-type: none;
}
```

### idセレクタに直接スタイルを当てない

スタイル設定に、直接idセレクタは使用すると以下のようなデメリットがあるので避ける。

- idセレクタはスタイルの詳細度を不必要に高めてしまうのであとから調整がききにくくなる。
- 同じidは1ページにつき１つという決まりがあるためスタイルの再利用がしにくくなる。

idはページ内リンクやJavaScriptでのDOM操作のみに使用する。

```
/* 【NG】idにスタイルを当てている */
#top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

### idセレクタ経由でスタイルを当てる場合

- 非推奨としている会社もあるが、可とする。
- この場合にidを指定する際は、ハイフン「-」を指定することを推奨。
- ハイフンを使用することで、Javascriptの動作対象から外れるため、意図しないJavascriptの動作に巻き込まれることが避けられる。

[Google HTML/CSS Style Guide（id Attributes）](https://google.github.io/styleguide/htmlcssguide.html#id_Attributes)


```
/* 【可】idセレクタ経由でスタイルを当てている */
#top-page h1 {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

### セレクタのネスト（入れ子）はほどほどに

セレクタを過剰にネストするとスタイルの影響範囲がわかりづらくなったり、コードの可読性が悪くなったりするため、 メンテナンスがしにくいCSSになってしまう。それに加えて、ネストが深いCSSはCSSの読み込み速度を低下させるデメリットもある。　　
以上の理由から、セレクタのネストが深くなりすぎないように注意することが望ましい。具体的には、ネストをする際は以下のように孫セレクタまでに留めることを推奨する。

```
親 > 子　> 孫
```

そもそもBEMやSMACSSなどのルールに基づいてクラスを命名していれば、ネストはあまり使う必要がなくなる。


### モジュールごとにスタイルをつける
スタイルは原則としてモジュールごとに定義する。Utilityクラス中心のスタイリングは推奨しない。  
Utilityクラスとは、特定の一つのCSSプロパティだけが割り当てられたクラスのこと。(Helperクラスと言う場合もある。)  
Utilityクラスは部分的に使うと便利な時があるが、乱用すると細かい調整が必要になった時に修正がしづらいので多用することは避ける（使用は可）。

- ▽NG Utilityクラスを多用してスタイリングしている

```
<div class="mb50 bold bg-gray p10">
　Hello, world!
</div>
```

```
.mb50 { margin-bottom: 50px; }
.p10 { padding: 10px; }
.bold { font-weight: bold; }
.bg-gray { background-color: #ddd; }
```

- ▽OK モジュールごとにスタイリングしている

```
<div class="message-box">
　Hello, world!
</div>
```

```
.message-box {
  padding: 10px;
  margin-bottom: 50px;
  font-weight: bold;
  background-color: #ddd;
}
```

### インラインスタイルは原則使用しない
スタイルの記述場所が分散するため、インラインスタイルは原則使用しない。<br>ただし、状況によってはbackground-imageなどはインラインスタイルで使用しても良い。

- ▽NG (インラインスタイルを使用している)

```
<div class="message-box" style="color: red">
　Hello, world!
</div>
```

### 単位に関する注意事項

#### font-size

固定値で指定する際は、remで設定する。htmlタグに font-size: 62.5%; を指定することで、1.6rem = 16px と計算される。
    
```
html {
  font-size: 62.5%;
}

.text-test {
  font-size: 1.6rem; /* 16px */
  font-size: 1.8rem; /* 18px */
  font-size: 2rem; /* 20px */
}

```

#### vwを使用する場合

スマホ・タブレット用のコーディングで普通の段落文字のfont-sizeをvwで指定する場合は、画面幅によって文字の大きさが極端に大きくなる、小さくなることを避ける。

▽例1：font-sizeの最小値と最大値を指定する。

[MMD clamp()](https://developer.mozilla.org/ja/docs/Web/CSS/clamp)

```
font-size: clamp(16px, 5vw, 20px); /* 16px以下にはならず、20pxを超えない */
```

```
font-size: clamp(16px, calc(18 / 384* 100vw), 18px); /* ブラウザが384px以下になると18pxが縮小する。しかし、16px以下にはならず、18pxを超えない。 */
```

▽例2：ブラウザ幅以下になった時の指定。
```
font-size: min(40 / 1920* 100vw, 40px); /* ブラウザ幅が1920px以下になった際、40pxがブラウザ幅に応じて縮小する */
font-size: min(30 / 1440* 100vw, 30px); /* ブラウザ幅が1440px以下になった際、30pxがブラウザ幅に応じて縮小する */
font-size: min(20 / 384* 100vw, 20px); /* ブラウザ幅が384px以下になった際、20pxがブラウザ幅に応じて縮小する */
```

[MMD min()](https://developer.mozilla.org/ja/docs/Web/CSS/min)

#### line-height
単位なしの相対値で設定する。pxなどの固定値で設定しない。
<b>OK</b>　line-height: 1.6;
<b>NG</b>　line-height: 20px;

#### letter-spacing
OK letter-spacing: 0.04em
NG letter-spacing: 1px


### リセットCSSを使用する
新規のコーディングプロジェクトにはリセットCSSを使用する。（時代によって変化するため、最新の情報を確認すること）

おすすめのリセットCSS

- [destyle.css](https://github.com/nicolas-cusan/destyle.css/blob/master/destyle.css)
- [coliss](https://coliss.com/articles/build-websites/operation/css/css-reset-for-modern-browser.html)


### Sassについて
Sassで書かれたサイトを編集する際は、原則Sassファイルを修正すること。  
style.cssを直接修正すると、Sassファイルを更新した際に上書きがされる恐れがある。

詳しくは[こちらの](https://github.com/mukai-chirashiya/style-guide/blob/master/HTML-CSS.md#sass%E3%81%A7%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%AB%E3%82%92%E6%9B%B8%E3%81%8F)ガイドラインを見る。

### レスポンシブ対応について
####ブレイクポイント
PC用、タブレット用、スマホ用の３種類のデバイスに対応できるようにスタイルを組む。  
ブレイクポイントはデザイン応じて適したものを選ぶ。

```
@media screen and (max-width:767px){}
```

#### メディアクエリはモジュール単位で記述する。
メディアクエリをブレイクポイントごとにすべてまとめて記述する方法は表示速度の点ではやや有利だが、 メンテナンス性が良くないのでモジュールごとに記述すること推奨する。  
Sassを使用している場合は要素ごとにミックスインをインクルードしてメディアクエリ用のスタイルを書く。

```
/* CSSの場合 モジュールごとにメディアクエリを指定　*/
.top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 38px;
  letter-spacing: 0.04em;
}

@media screen and (max-width: 1199px){
  .top-level-heading {
    padding: 5px 0;
    font-size: 27px
  }
}

@media screen and (max-width: 767px){
  .top-level-heading {
    font-size: 22px
  }
}

.data-list {
  margin-bottom: 50px;
  padding: 10px;
  background-color: #ddd;
}

.data-list__title {
  font-weight: bold;
  font-size: 24px;
}

@media screen and (max-width: 1199px){
  .data-list {
    padding: 5px;
  }

  .data-list__title {
    font-size: 20px;
  }
}

@media screen and (max-width: 767px){
  .data-list__title {
    font-size: 16px;
  }
}
```

### ブラウザサイズについて
- 基本的に1920px〜350pxのブラウザに対応する。
- 2560pxのブラウザサイズに広げても、表示に崩れがないこと。  
[最新のディスプレイサイズシェア動向](https://support.neoworks.jp/website/website-website/website-prepare/tends/)  
[statcounter](https://gs.statcounter.com/screen-resolution-stats)  


### インナー幅について
基本的に1200px 〜 1024pxの間で対応する。  
※インナー幅は必ず引くこと。
```
/* OK例 */
.inner {
  max-width: 1200px;
  width: 100%;
  margin-inline: auto;
}
```
なお、インナー幅を力技で中央寄せに見せることはNGとする。
```
/* NG例 */
.inner {
  max-width: 1200px;
  width: 100%;
  margin-left: 30%;
}
```

### 余白の方向について

下方向に統一すること。
マージンの相殺が起こるため、上と下方向の指定が混ざることは非推奨。
[MMD margin](https://developer.mozilla.org/ja/docs/Web/CSS/margin#%E3%83%9E%E3%83%BC%E3%82%B8%E3%83%B3%E3%81%AE%E7%9B%B8%E6%AE%BA)

```
/* OK例 */
.test {
  margin-bottom: 50px;
}

.test2 {
  margin-bottom: 30px;
}
```

```
/* 非推奨例 */
.test {
  margin-bottom: 50px;
}

.test2 {
  margin-top: 30px;
}
```

### width、heightの固定値について

ブラウザサイズを狭めたときに見切れる、レイアウトの崩れが発生する可能性があるため、固定値での指定はなるべく回避する。  
特に要素を囲む箇所にheightを固定値で指定すると、後から中の要素が増えたときに、増えた分がはみ出す可能性があるため、非推奨とする。

```
<section class="test">
  <p>テスト</p>
</section>
```

```
/* 非推奨例 */
.test {
  height: 200px 
}
```

```
/* 可 */
.test {
  min-height: 200px
}
```

```
/* 可 */
.test {
  padding: 100px 0; /* paddingで余白を作る */
}
```

### ボタンについて

width、heightの固定値は極力使わず、paddingを指定する。
固定値を使うと、ボタン内の文字数が増えたり文字が改行された際に、ボタンから文字がはみ出す恐れがある。

```
<div class="btn">
  <a href="" class="btn-link">実績一覧を見る</a>
</div>
```

```
/* OK例 */
.btn-link {
  padding: 10px 25px;
  min-width: 300px;
}
```

```
/* 非推奨例 */
.btn-link {
  width: 350px;
  height: 60px;
}
```

### OGP画像、ファビコン、ウェブクリップ画像について

※OGP、ファビコンは納品前に必ずサイトに反映する。

- OGP画像：1200×630px で作成。
- ファビコン：32x32 で作成。
- ウェブクリップ：180x180px で作成（こちらは可能であれば用意する）

[Faviconジェネレーター](https://favicon-generator.mintsu-dev.com/)


### title、meta属性について

ちらし屋式（仕事のルール）という名称のガイドラインがあるため、そちらの内容を確認すること。

### CSSフレームワーク

CSSフレームワークの導入は非推奨。導入前は社内で確認すること。

- [Bootstrap](https://getbootstrap.jp/)
- [tailwindcss](https://tailwindcss.com/)

