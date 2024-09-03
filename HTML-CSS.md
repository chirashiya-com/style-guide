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
  <li><b>OK</b> heading image</li>
  <li><b>OK</b>midashi gazou</li>
</ul>

