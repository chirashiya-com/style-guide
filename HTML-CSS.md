<h1>ちらし屋HTML/CSSスタイルガイド 2024年作成</h1>

<ol>
  <li><a href="#start">はじめに</a></li>
  <li><a href="#policy">基本方針</li>
  <li><a href="#rule">HTML/CSS基本ルール</li>
  <li><a href="#style-guide">CSSのスタイルガイド</li>
</ol>

<h2 id="start">1.はじめに</h2>

<p>HTML/CSSのコーディングは自由度が高いため、コーダーが独自のルールで書くと修正や拡張がしにくいコードが作られがちです。<br>
そのような事態を回避するには、一貫した規則や設計のもとにコードを書くことが重要です。<br>
一貫したルールや設計のもとでコードを書くことにより以下のような効果が期待できます。</p>

<ul>
  <li>コードの品質を一定以上にたもつことができる。</li>
  <li>保守や修正にかかる労力を削減することができる。</li>
  <li>コードを書く際の迷いが減るため開発スピードが向上する。</li>
</ul>

<p>本ドキュメントでは、メンテナンス性が高いコードを書くために重要だと思われるポイントをスタイルガイドとしてまとめました。
なお、本スタイルガイドは以下のドキュメントや記事を参考に作成しています。</p>

<a href="https://google.github.io/styleguide/htmlcssguide.html" target="_blank" rel="noopener noreferrer">Google HTML/CSS Style Guide</a>


<h2 id="policy">2.基本方針</h2>
<h3>メンテナンス性の高いコードを書く</h3>
<ul>
  <li>一度書いたら終わりではなく、継続的に保守されることを前提にコードを書く</li>
  <li>自分以外の第三者が見ても理解できるコードを書くこと意識する。</li>
</ul>
<h3>ローカルルールも尊重する</h3>
<ul>
  <li>もし既存のコードに修正や追加をする場合は、まずコードを書く前にすでに書かれているコードを眺めて、使われている命名規則やコーディングスタイルを理解するように務める。<br>
もし一貫したルールの存在が認められる場合は、本スタイルガイドよりもローカルルールを優先してコードを書く方が良い。
  </li>
</ul>


<h2 id="rule">3.HMTL/CSS基本ルール</h2>
<h3>目的に応じたマークアップ(セマンティックなマークアップ)をする</h3>
<ul>
  <li>HTML要素は目的に応じたものを選んで使う。例えば見出しはh1～h6要素、段落にはp要素を使う、など。</li>
  <li>h1タグは1ページに1つのみ。重複している際は必ず修正する。</li>
  <li>よくあるケースがWordPressで、ロゴのh1タグとサブページ見出しのh1が被っていることがあるので注意。</li>
</ul>

<h3>構造がひと目でわかるようにインデントをつける。インデントはスペース２つにする</h3>
<ul>
  <li>コードを見て論理構造がわかるようにインデントをつける。</li>
  <li>ネストが深くなると読みにくくなるため、インデントはスペース２つを推奨する。<br>
    ※Visual Studio Codeなどのテキストエディタではネストの種類(スペースorタブ)や大きさ(何個分)か変更できる。
  </li>
</ul>

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
@meida screen and (max-width: 900px) {
  .logo {
    font-size: 24px;
  }
}
```

<h3>クラス名やID名の命名について</h3>
<h4>単語の区切りには-(ハイフン)を使う</h4>
<p>id名やクラス名に複数単語からなる語を当てる場合、記法単語の区切りは原則ハイフンを用いる。</p>

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

<h4>目的に応じたわかりやすい名前をつける</h4>
<p>ハンバーガーボタンのクラス / IDのネーミング例</p>

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

<h4>ローマ字での命名はしない</h4>
<ul>
  <li><b>OK</b>　heading image</li>
  <li><b>NG</b>　midashi gazou</li>
</ul>

<h3>画像の取り扱いについて</h3>
<ul>
  <li>画像を使わずともCSSで再現できそうなものはできるだけCSSで再現するようにする。一般的にはCSSのほうがきれいに表示され、読み込み速度も速い。</li>
  <li>文字は原則として画像を利用すべきではなく、HTMLのテキストとして打ち込むべきである。<br>ただし、デザインで指定されているフォントが有料フォントの場合で、テキストの内容が変更される可能性が低い箇所については、<br>テキストを画像として配置しても良い。その場合、以下の点に注意する。
    <ul>
      <li>ファイル形式はPNGよりSVG形式が望ましい</li>
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

<a href="https://github.com/chirashiya-com/style-guide/blob/main/IMAGE.md">jpg、pngの使い分けについて</a>

<h4>img要素にはalt属性を必ずつける</h4>
<p>※altに入れるテキストが不明な場合は、納品までに必ず確認して入れること。altが空のまま納品しない。</p>

```
<!--【OK】-->
<img src="./images/sample.png" alt="サンプル画像">
```

```
<!--【OK】画像に関する説明が不要であれば、alt属性の値は空でもOK(※alt属性自体の省略はNG) -->
<img src="./images/foo.png" alt="">
```

<h4>img要素にはwidth属性とheight属性を必ず記述する</h4>
<ul>
  <li>ページの読み込み速度に有利と言われている。<br>また、SVG形式の画像や、2xの解像度で書き出した画像のデフォルトの大きさを設定するのに使うと便利。</li>
  <li>width、height属性の記述がない場合、ブラウザが画像サイズを再計算する動作が生じるため、読み込み速度に影響が出ると言われている。</li>
  <li>
    <a href="https://coliss.com/articles/build-websites/operation/work/avoiding-img-layout-shifts.html">レイアウトシフトの防止になるため</a>
  </li>
</ul>

```
<!--【OK】width、heightの両方必須 -->
<img src="./images/sample.png" alt="サンプル画像" width="120" height="60">
```


<h4>ブラウザに最初に表示される領域以外は、loading="lazy"を必ず記述する</h4>

```
<!--【OK】loading="lazy" -->
<img src="./images/sample.png" alt="サンプル画像" width="120" height="60" loading="lazy">
```

<h4>画像ファイルの命名</h4>
<p>役割が分かるように接頭辞を入れることを推奨する。<br>ファイル内に並ぶ画像もabc順になるため、画像の管理がしやすくなる。</p>
<p>接頭辞の例</p>
<ul>
  <li>ico- アイコン（例 ico-star.png）</li>
  <li>pic- 写真 または img- 写真</li>
  <li>txt- テキスト</li>
  <li>bg- 　背景</li>
  <li>arw- 矢印<br>など</li>
</ul>

<h3>mp4動画について</h3>

20MB以下に抑えるように圧縮する。

<h3>a要素にtarget="_blank"属性を付ける場合は、rel="noopener noreferrer"属性もつける</h3>
<p>XSS攻撃に対する脆弱性を防ぐため。</p>

```
<!--【OK】-->
<a href="https://www.example.com/" target="_blank" rel="noopener noreferrer">新しいタブで開く</a>
```

```
<!--【NG】-->
<a href="https://www.example.com/" target="_blank">新しいタブで開く</a>
```

<h3>HTMLを一通り書いてからCSSを書く（任意）</h3>
<p>HTMLとCSSは同時に書くのは避ける。HTMLとCSSを並行して書くと、設計にブレが生じやすく、コーディングスピードも遅くなる。<br>
HTMLを書き終わってからCSSを書くほうが、設計に一貫性をもたせやすく、コーディング完了までのスピードも速くなる。</p>


<h2 id="style-guide">4. CSSのスタイルガイド</h2>
<p>GoogleのエンジニアPhilip Waltonによる記事「<a href="https://philipwalton.com/articles/css-architecture/">CSS Architecture</a>」では、CSSを設計する時に目指すべき４つのゴールが紹介されている。</p>
<ul>
  <li>予測しやすい - クラス名や構造などからふるまいを容易に想像できる。</li>
  <li>再利用しやすい - 必要に応じて他の場所でも同じように使いまわしができる。</li>
  <li>保守しやすい - 新たな要素を追加したり、既存の要素を修正したりしたりした時に、他の要素を壊すことがない。</li>
  <li>拡張しやすい - 誰かがCSSを後に編集することになっても、容易に編集できる。</li>
</ul>
<p>このCSSスタイルガイドもこれらのゴールを満たすCSSを書くことを目指している。</p>

<h3>CSSの基本フォーマット</h3>
<p>以下のフォーマットに従って書く。</p>

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

<h3>適宜コメントを入れる</h3>
<p>スタイルが何のためのものなのかわかるようにCSSファイルに適宜コメントを書くようにする。</p>
<ul>
  <li>コメントの例</li>
</ul>

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

<h3>不要なスタイルの重複記述を避ける</h3>
<p>不要な重複記述は保守性を悪化させるため、不必要なスタイルの記述の重複がないようする。</p>

```
/*【NG】無駄な重複がある。 */
.text {
  margin-bottom: 20px;
  color: #333;
  font-size: 24px;
  line-height: 1.6;
  letter-spacing: 0.01em;
}

@media screen and (max-width: 900px) {
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

@media screen and (max-width: 900px) {
  .text {
    font-size: 20px;
    margin-bottom: 14px; 
  }
}
```

<h3>スタイルは原則クラスに当てる</h3>
<p>スタイルは原則としてクラスに記述する。 スタイルをクラスに当てることは以下のようなメリットがある。</p>
<ul>
  <li>スタイルの影響範囲を限定できる</li>
  <li>スタイルの再利用がしやすい</li>
  <li>スタイルの詳細度をある程度一定に保つことができるので、上書きや変更がしやすい。</li>
</ul>
<p>idセレクタや要素セレクタにスタイルを当てることのデメリットについては後述する。</p>

```
/* 【OK】クラスセレクタにスタイルを当てている */
.top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

<h3>クラスの命名には一貫した命名規則を採用する</h3>
<ul>
  <li>メンテナンス性の高いCSSを書くには、クラスの命名に一貫したルールをもたせるのが非常に重要である。</li>
  <li>クラスの命名規則に特に指定はないが、必ず命名に一貫したルールをもたせること。</li>
  <li>代表的な命名規則を挙げるが、導入前は社内で確認をすること。（BEM、OOCSS、SMACSS、FLOCSS）</li>
</ul>


<h3>要素セレクタを併記しない</h3>
<p>スタイルが要素名に依存してしまうのでNG。<br>
例えば以下の例だと、HTML側でh1をpに変更した場合、スタイルが効かなくなってしまうので、メンテナンス性が悪い。</p>

```
/* 【NG】要素セレクタを併記している */
h1.top-level-heading {
  padding: 10px 0;
  font-size: 20px;
  letter-spacing: 0.04em;
  text-align: center;
}
```

<h3>要素セレクタ単体にスタイルを当てない</h3>
<p>要素セレクタ単体にスタイルを当てると、影響範囲が広すぎるため意図しないところでのスタイルが崩れる可能性がある。<br>
要素セレクタ単体にスタイルを当てるのは、スタイルをリセットするときのみにする。</p>

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
<p>▽要素セレクタにリセット用のスタイルを設定するのはOK</p>

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

<h3>idセレクタに直接スタイルを当てない</h3>
<p>スタイル設定に、直接idセレクタは使用すると以下のようなデメリットがあるので避ける。</p>
<ul>
  <li>idセレクタはスタイルの詳細度を不必要に高めてしまうのであとから調整がききにくくなる。</li>
  <li>同じidは1ページにつき１つという決まりがあるためスタイルの再利用がしにくくなる。</li>
</ul>
<p>idはページ内リンクやJavaScriptでのDOM操作のみに使用する。</p>

```
/* 【NG】idにスタイルを当てている */
#top-level-heading {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

<h3>idセレクタ経由でスタイルを当てる場合</h3>
<ul>
  <li>非推奨としている会社もあるが、可とする。</li>
  <li>この場合にidを指定する際は、ハイフン「-」を指定することを推奨。</li>
  <li>ハイフンを使用することで、Javascriptの動作対象から外れるため、意図しないJavascriptの動作に巻き込まれることが避けられる。</li>
</ul>
<p><a href="https://google.github.io/styleguide/htmlcssguide.html#id_Attributes">Google HTML/CSS Style Guide（id Attributes）</a></p>

```
/* 【可】idセレクタ経由でスタイルを当てている */
#top-page h1 {
  padding: 10px 0;
  text-align: center;
  font-size: 20px;
  letter-spacing: 0.04em;
}
```

<h3>セレクタのネスト（入れ子）はほどほどに</h3>
<p>セレクタを過剰にネストするとスタイルの影響範囲がわかりづらくなったり、コードの可読性が悪くなったりするため、 メンテナンスがしにくいCSSになってしまう。それに加えて、ネストが深いCSSはCSSの読み込み速度を低下させるデメリットもある。<br>
以上の理由から、セレクタのネストが深くなりすぎないように注意することが望ましい。具体的には、ネストをする際は以下のように孫セレクタまでに留めることを推奨する。</p>

```
親 > 子　> 孫
```

<p>そもそもBEMやSMACSSなどのルールに基づいてクラスを命名していれば、ネストはあまり使う必要がなくなる。</p>


<h3>モジュールごとにスタイルをつける</h3>
<p>スタイルは原則としてモジュールごとに定義する。Utilityクラス中心のスタイリングは推奨しない。<br>
Utilityクラスとは、特定の一つのCSSプロパティだけが割り当てられたクラスのこと。(Helperクラスと言う場合もある。)<br>
Utilityクラスは部分的に使うと便利な時があるが、乱用すると細かい調整が必要になった時に修正がしづらいので多用することは避ける（使用は可）。</p>

<ul>
  <li>▽NG Utilityクラスを多用してスタイリングしている</li>
</ul>

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

<ul>
  <li>▽OK モジュールごとにスタイリングしている</li>
</ul>

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

<h3>インラインスタイルは原則使用しない</h3>
<p>スタイルの記述場所が分散するため、インラインスタイルは原則使用しない。<br>ただし、状況によってはbackground-imageなどはインラインスタイルで使用しても良い。</p>
<ul>
  <li>▽NG (インラインスタイルを使用している)</li>
</ul>

```
<div class="message-box" style="color: red">
　Hello, world!
</div>
```

<h3>単位に関する注意事項</h3>
<h4>font-size</h4>
<p>固定値で指定する際は、remで設定する。htmlタグに font-size: 62.5%; を指定することで、1.6rem = 16px と計算される。</p>
    
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

<h4>vwを使用する場合</h4>
<p>スマホ・タブレット用のコーディングで普通の段落文字のfont-sizeをvwで指定する場合は、画面幅によって文字の大きさが極端に大きくなる、小さくなることを避ける。</p>

▽例1：font-sizeの最小値と最大値を指定する。

<p><a href="https://developer.mozilla.org/ja/docs/Web/CSS/clamp">MMD clamp()</a></p>

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
<p><a href="https://developer.mozilla.org/ja/docs/Web/CSS/min">MMD min()</a></p>


<h4>line-height</h4>
単位なしの相対値で設定する。pxなどの固定値で設定しない。
<b>OK</b>　line-height: 1.6;
<b>NG</b>　line-height: 20px;

<h4>letter-spacing</h4>
OK letter-spacing: 0.04em
NG letter-spacing: 1px


### リセットCSSを使用する
<p>新規のコーディングプロジェクトにはリセットCSSを使用する。（時代によって変化するため、最新の情報を確認すること）</p>
<p>おすすめのリセットCSS</p>
<ul>
  <li><a href="https://github.com/nicolas-cusan/destyle.css/blob/master/destyle.css">destyle.css</a></li>
  <li><a href="https://coliss.com/articles/build-websites/operation/css/css-reset-for-modern-browser.html">coliss</a></li>
</ul>

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
