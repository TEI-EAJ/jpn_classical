# 日本語古典籍TEI本文データ作成要領
NIJL-NW TEI Project / TEI-C SIG EA/JP / SAT Project

2019.11.5 (初版)

2020.2.12 (改訂1版)

## 本資料の目的
本資料は、納入された本文データが適切に作成されたものであるかどうかの判断材料として作成されるものである。本資料に記載がなくとも、本文作成およびデータ作成上の常識に照らして不適切である場合は、本資料によらず不適切と判断することがある。仕様書と記載が食い違う場合は仕様書が優越する。
### 用語
* 翻刻
	* 異なるメディアからメディアに情報のデータ形式を変換すること。ここでは、なんらかのメディアで運搬されているテクストを現行のコンピュータ上の文字に変換することをいう。翻刻が厳密であるとは、変換に際しての恣意をなるべく排したものであることを謂う
* 校本
	* 比校すべき異文が一つのファイルにおいて符号化された電子的テクスト
* 整定本文
	* 本文の読みが整理され、論理構造が符号化された電子的テクスト
* 読み下し
	* 漢文的に書かれた本文が日本語の語順で読めるように解釈された電子的テクスト
* 解釈本文
	* 原本画像をもとに厳密に翻刻をし、それに解釈を施して適宜漢字を宛て、句読を示し、清濁や仮名遣いをただした本文を記した電子的符号化テクスト
* 校訂本文
	* 原本画像をもとに厳密に翻刻をし、参照すべき適当な他本との比校によって改訂した本文を記した電子的符号化テクスト
* 生成版
	* 翻刻を基礎とし、手稿内における内容の発展を符号化した電子的テクスト
* 符号化レベル
	* 段階を踏んで基礎的なものから詳細なものへと符号化を進めるという考え。古典籍の翻刻については、TEIベース写本翻刻タグセット、EpiDocをも参照のこと。
	* 本文書では、以下のレベルを想定する。
		* Lv. 1 OCRテキスト
		* Lv. 2 翻刻・校本
			* Lv. 2a 翻刻
			* Lv. 2b 校本
		* Lv. 3 整定本文（下位レベルに上下はない）
			* Lv. 3a 解釈本文
			* Lv. 3b 読み下し
			* Lv. 3c 校訂本文
		* Lv. 4 注釈つき本文
			* Lv. 4a 本文中の情報を識別する符号化がされている
			* Lv. 4b 本文中の情報に対して情報が付加されている
## データ作成要領
### 一般論
* 基本的なTEI作成に必要な事柄を守る
	* 以下の記載では&lt; &gt;で要素を、@で属性を示す。P5とあるのはTEI P5 Guidelinesの章である。TEIのバージョンは3.6.0とする
* 使用字体は大別して以下のいずれかの方向性があり得るが、今回の翻刻では後者とする。
	* 資料において書き様において異なる字形群（字体）を電子的に可能ななんらかの手段で表記し分ける。また、必要に応じて、仮名字母の表記、旧字体・新字体などを区別した表記などの簡易表記も考えられる。 
	* 使用字体は通行のものとし、表現効果を持つと論証される場合を除いて原文の趣をしいて保存することはしない
* 校訂に際しては、それによって写本系統の主要な異同が知られ、かつ、本文の読みを確立することを目的とする
### ヘッダー(&lt;header&gt;)
符号化に関する記述(&lt;encodingDesc&gt;; cf. P5 Ch. 2 §3)
* 符号化に際して立てた方針を、符号化担当者でない人に理解できるように丁寧に解説する
* 字体・字形の使用方針について明確に記述する（テクスト作成時の方針について記載すればよく、正確性・網羅性は求めない）
底本の書誌記述(&lt;sourceDesc&gt;/&lt;msDesc&gt;; cf. P5 Ch. 10)
* 所蔵歴・来歴・書名・書写年代・装訂・料紙・法量・書写形態・補筆・鑑定などの本文に関する基本事項を過不足なく記載のこと
* 記載すべきと判断したおりには、適切な要素で符号化することを要する
* 校訂本文においては、異本の情報をsourceDesc下のlistWitにおいて&lt;witness&gt;を用いて書誌情報とともに適切に符号化する(cf. P5 §12.1.4.3)。詳細にわたることは要しないが、対校に適切な理由が分かるものである必要がある
### 本文(&lt;text&gt;)
* 原文の各行は行頭に&lt;lb/&gt;を付する。
* 底本の半丁ごとに境目を&lt;pb/&gt;で示し、@nで丁番号ないし仮の墨付きの丁数を示す。
* 短歌は全部を&lt;l&gt;で区切り、長歌は&lt;lg&gt;で符号化し、&lt;l&gt;で内部を区切る。
	* 上の句／下の句の境で改行されていると解釈できるばあいは、&lt;l&gt;を分けるが、それ以外の改行は&lt;lb/&gt;で行を示す。
* 章段を設定し、章を&lt;div&gt;で、段を&lt;p&gt;で符号化する。章段をあながちに設定しないばあいは、&lt;ab&gt;で一定のまとまりを符号化する。
* 解釈本文においては解釈本文のみを示し、整定前の本文は&lt;text&gt;の次に&lt;sourceDoc&gt;によって示す。解釈の正当化をするばあいは&lt;note&gt;によって説明する。
* 校訂本文においては校訂を行った箇所を&lt;app&gt;で示し、本文を&lt;lem&gt;、必要な異文（あるいは底本原文）を&lt;rdg&gt;で符号化する。
	* 校訂にかかる箇所は、&lt;respStmt&gt;によって記述される校訂者情報のxml:idをresp属性によって示すものとする。
* また、上記にかかわらず、あきらかな誤字は&lt;choice&gt;のもとに&lt;sic&gt;および&lt;corr&gt;で正すものとする。
* 虫損等で読めない箇所は、&lt;gap&gt;要素に適切な情報を与えることで記述する。他本によって補えるばあいは、&lt;damage&gt;要素で欠損の範囲を符号化したうえで、&lt;supplied&gt;要素によって補う。このほか，判断によって補った本文は基本的に&lt;supplied&gt;で示す。
* 補写は開始時点を&lt;handshift&gt;で記載する。他筆について分ることは，&lt;handNote&gt;において情報を示すものとする
### 注記
注記は内容によってマークアップを変えることを原則とする。
#### 割り書き
割り注については，&lt;note&gt;で符号化し，@rendを"double_line"や"three_line"，"割注"などとする。
角書きなどについては，適当な要素によって符号化するが，どうしても表現できないばあいは&lt;seg&gt;で仮に@typeを"角書"などとする。
#### 書き直し（P5 Ch. 11 §3）
書き直しについては，基本的に&lt;subst&gt;で影響する範囲を符号化し（どちらがよいと判断できない・判断を避けるばあいは&lt;mod&gt;を用いることができる），&lt;del&gt;と&lt;add&gt;によって削除された本文と加筆された本文とを明記する。このとき，加筆された本文がどこにあるかを@placeによって示すことができる。削除が，抹消ではなく見せ消ちのばあいは&lt;del&gt;の@rendを"見せ消ち"などとする。
上書きは&lt;retrace&gt;で符号化するが，不明瞭な箇所に傍書して書き直したようなばあいは、&lt;unclear&gt;と&lt;add&gt;によって関係を示す。
加筆や削除が広汎にわたるばあいは，&lt;delSpan&gt;と&lt;addSpan&gt;，&lt;anchor&gt;で範囲を示し，&lt;zone&gt;にその範囲の本文を示す。このとき，&lt;metamark&gt;でその削除の様態を示すことができる。
#### 異本注記

```xml
<p>
    さだめなり<seg xml:id="w1">けり</seg>
    <add xml:id="w2" place="right" corresp="#w1">
        <metamark fuction="他本">亻</metamark>けるを
    </add>
</p>
<alt target="#w1 #w2" mode="excl" /> 
```


```xml

<p>
    さだめなり
    <note targetEnd="#w1e" place="right">
    <metamark fuction="他本">亻</metamark>
    けるを
    </note>けり<anchor type="noteEnd" xml:id="w1e"/>
</p>
```

# 場所は分かりやすければ、段落直後でも、末尾に一括しても
その他の自筆・他筆の書き入れ（P5 Ch. 11 §3）
本文に対する単純な内容であれば、`<add>`によって示す。欄外に見出しや頭注を示すようなばあいは，原本の記述であれば`<label>`で示し，本文の一部とするばあいは`<head>`や`<note>`で示す。
原文のその他の注記は、一般的に、関係する箇所に&lt;note&gt;で記述し、@rendによって場所を示す。また，他筆は上記の補筆と同様に考え，@changeや@handによって示すことができる。
校訂者の付けた注は必要な`@resp`を附す。
### Misc
#### 振り仮名（当面）
`<seg type="furigana">` `<seg type="furigana_body">`本行`</seg>` `<seg type="furigana_text">`振り仮名`</seg>` `</seg>`のように符号化する。
これではじゅうぶんに符号化されないばあいは協議するものとする。
### 訓点
たとえば、楚人有㆘鬻㆓盾與一レ矛者上とあるとき、以下のように符号化することができる（訓読をテクストとして保存しない際は、prev、next属性を省くことができる）。より簡易にはwではなくanchorとmetamarkの組み合わせでも実現は可能であろう。返り点は可能なかぎりユニコードの専用の文字を使うべきである。

```xml
         <p>
            <w xml:id="w1">楚人</w>
            <w xml:id="w2">有</w>
            <metamark function="transposition" target="#w2" place="margin-left"
               prev="#w3">㆘</metamark>
            <w xml:id="w3">鬻</w>
            <metamark function="transposition" target="#w3" place="margin-left"
               prev="#w4">㆓</metamark>
            <w xml:id="w4">盾</w>
            <w xml:id="w5">與</w>
            <metamark function="transposition" target="#w5" place="margin-left"
               prev="#w6" next="#w3">㆒㆑</metamark>
            <w xml:id="w6">矛</w>
            <w xml:id="w7">者</w>
            <metamark function="transposition" target="#w7" place="margin-left"
               next="#w2">㆖</metamark>
         </p>
```

あるいは、訓読をして、
	 
```xml
         <p>
            <w xml:id="w1">
               <seg type="ruby">
                  <seg type="rb">楚人</seg>
                  <seg type="rt">そじん</seg>
               </seg>
               <add>ニ</add>
            </w>
            <w xml:id="w2">
               <seg type="ruby">
                  <seg type="rb">有</seg>
                  <seg type="rt">あ</seg>
               </seg>
               <add>リ</add>
            </w>
            <metamark function="transposition" target="#w2" place="margin-left" prev="w3">㆘</metamark>
            <w xml:id="w3">
               <seg type="ruby">
                  <seg type="rb">鬻</seg>
                  <seg type="rt">ひさ</seg>
               </seg>
               <add>グ</add>
            </w>
            <metamark function="transposition" target="#w3" place="margin-left" prev="w4">㆓</metamark>
            <w xml:id="w4">
               <seg type="ruby">
                  <seg type="rb">盾</seg>
                  <seg type="rt">たて</seg>
               </seg>
            </w>
            <w xml:id="w5">
               <seg type="ruby">
                  <seg type="rb">與</seg>
                  <seg type="rt">と</seg>
               </seg>
               <add>ヲ</add></w>
            <metamark function="transposition" target="#w5" place="margin-left" prev="w6" next="#w3">㆒㆑</metamark>
            <w xml:id="w6">
               <seg type="ruby">
                  <seg type="rb">矛</seg>
                  <seg type="rt">ほこ</seg>
               </seg>
            </w>
            <w xml:id="w7">
               <seg type="ruby">
                  <seg type="rb">者</seg>
                  <seg type="rt">もの</seg>
               </seg>
            </w><metamark function="transposition" target="#w7" place="margin-left" next="#w2">㆖</metamark>
         </p>
```
というように符号化することができる。
### ID
xml:id属性を附す。
