<h1>ちらし屋HTML/CSSスタイルガイド 2024年作成</h1>

<ol>
  <li><a href="#start">はじめに</a></li>
  <li><a href="#policy">基本方針</li>
  <li><a href="#rule">HTML/CSS基本ルール</li>
  <li><a href="#style">CSSのスタイルガイド</li>
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


<h2 id="rule">HMTL/CSS基本ルール</h2>
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







