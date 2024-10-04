<script type="text/x-mathjax-config">MathJax.Hub.Config({tex2jax:{inlineMath:[['\$','\$'],['\\(','\\)']],processEscapes:true},CommonHTML: {matchFontHeight:false}});</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML"></script>

# AtCoder青色になった！

## はじめに

　青色コーダーになった！（爆速タイトル回収）
入水が2023/07/29で入青が2024/08/10だからちょうど一年くらい水色だったらしい．
初めて色変記事の執筆に挑戦！（文章の後半に漫画「鬼滅の刃」のネタバレを含みます）

## 入水時点から何が成長したのか

### 典型力の向上

　典型90の☆5〜☆6，ABCの水diffと青1〜2diffの問題を解いた．
水diffを解くのに必要なアルゴリズムや典型テクニックを身につけることができたと思う．
典型90の☆5の内容はだいぶ使いこなせるようになったが，典型90の☆6はまだあまり身に付いてないと思う．
以下に覚えたテクニックをいくつか挙げる．
矢印を使っているが左側と右側は一対一対応ではないことに注意していただきたい．
そして，過学習気味なところもあると思うから注意して欲しい．

- 数列の順番が関係ない → ソートしたほうが考えやすい
- XOR → ビット毎に考える
- グラフ上の辺の破壊クエリ → 後ろから考える
- 回文 → 前半のみで一意に定まる
- 回文 → 長さが奇数と偶数の場合で分けて考える
- 最小全域木 → 辺の重みが軽い順の貪欲（クラスカル法の気持ちになる）
- Functional Graph → 各連結成分につき一つの閉路がある
- ゲームでの期待値 → 後ろからDP
- 解の候補が $N!$ 通りあり，それが「使用した要素の集合」と「最後の要素」にのみ依存する →  $2^NN$ 通りに落とすことができる
- 結合法則が成り立つ → 累積◯◯ができる（累積和，累積max，累積GCDなど）
- 結合法則が成り立つ → 単位元があればセグメント木に乗る
- DPで数え上げたいけど重複する → $DP[i]=◯◯の最大値がiになる場合の数$
- 各要素の重要度が選び方によらず一定 → ソートしてDP

　以上のように自分の中の典型はできる限り<span style="color: red; ">（条件） → （テクニック・事実）</span>の形式で理解するようにしている．
これは競プロのテクニックを覚えても，使い所が分からなければ意味がないと思うからだ．
それに加えて，「（条件）を満たすか？」を考えることは再現性のある考察に繋がると考えるからである．

　こういう考え方は「パターンマッチング」と言われ，上位帯に行けば行くほどレートが上がりにくいと言われている．
しかし，暖色コーダーが安定して短い時間で水diffを解いている事実からもある程度はパターンマッチをしていると思う．
パターンマッチングについて二つの考え方があり，これから競プロを続けるにあたってこの考え方が自分の中でどう変化するか楽しみだ．

### 数式力の向上

　問題内で式変形や式のイメージができるようになってきた気がする．
考察の途中で出てきた式に対して式変形やイメージをできることでスムーズに解ける問題もあるように感じる．
これも下にいくつか例を挙げてみる．

### 式変形

- $\sum_{x}{kf(x)}=k\sum_{x}{f(x)}$（ $\sum$ に関係ない値は外に出せる．）
    - $\sum{|X-x_i|+|Y-y_i|}=\sum{|X-x_i|}+\sum{|Y-y_i|}$ 
    （マンハッタン距離の総和における $X$ 軸， $Y$ 軸の分離）

- $\sum^{N}_{L=1}{\sum^{N}_{R=L}{f(L,R)}}=\sum^{N}_{R=1}{\sum^{R}_{L=1}{f(L,R)}}$
（ $L$ を固定 → $R$ を固定）

- $\sum^{N}_{k=0}{\binom{N}{k}}=2^N$ 　　（ $O(N)$ が 繰り返し二乗法で $O(\log N)$ になる！）

### イメージ

- $ax+by+c=0$ → 直線だな〜単調性あるから二分探索かな〜
- $y=ax^2+bx+c$ → 放物線だな〜どっちに凸だろうな〜線対称な形だな〜
- $A \le x \le B$ かつ $C \le y \le D$ → 長方形だな〜
- $\sum^{R}_{i=L}{A_i}$ → 配列 $A$ に変更がないなら累積和，変更があるならBITで高速に求まるな〜

### 問題文の言い換え

　競プロでは問題文や考察中に出てくる条件や処理をどれだけ取り扱いやすい形に言い換えることができるかがとても重要であると考える．
この章では，言い換え力を鍛えるために参考にしている文章と意識していることを説明していこうと思う．

　まず，私が言い換え力が重要だと思うようになるきっかけでありお手本である「[問題文の読み方](https://codeforces.com/blog/entry/62730)」という文章を紹介する．
これはUm_nikさんという赤コーダーによって書かれた文章である．
ここでは私なりの要約と解釈を書いていくため，まず元の文章を読むことをお勧めする．

　私が「問題文の読み方」の文章のうち特に重要だと考える２つのトピックを以下に紹介する．

- 問題文を読んだ結果はたいてい数学的なモデルである．ストーリーが理解を助けるなら残して良いが，不要な細部はできるだけ削ぎ落とすようにする．
- 問題文で気に入らない部分があれば，気に入る言い方に変えてみる．対象を理解することから始めて，単純化する．このテクニックで完全に解ける問題もある．

　私は過去問を解く際やコンテストで実際に問題を解く際に，問題文を数学的なモデルに落とし込むことを意識することでレートが上がったように感じる．
これは以下の理由があると思う．

- 数式に落とし込んでから考察するから，実装がスムーズ
- 数式に落とし込もうとすることで，自分の中で理解できていない部分が明らかになり問題に取り組みやすくなる
- ストーリーが違っても数学的なモデルに落とし込むと同じ形になることがあり，考察に再現性が生まれる．
    - 例えば，「2次元平面上で $(X_1,Y_1)$ と $(X_2,Y_2)$ を対角線にもつ長方形」は数学的なモデルに落とし込むと「 $X_1 \le x \le X_2$ かつ $Y_1 \le y \le Y_2$ 」となる．
    - 一方，「開始時刻が $A$ から $B$ の間で，終了時刻が $C$ から $D$ の間となる区間」は数学的なモデルに落とし込むと「 $A \le begin \le B$ かつ $C \le end \le D$ 」となる．
    - 両者が同じ内容であることに気付くだろうか．数学的なモデルという統一されたフォーマットがあることで「これ見たことある！」が生まれやすい．

　また，多分，暖色コーダーたちは問題文を数学的なモデルに落とし込むことを意識せずとも行っているのだと思う．
[のいみさんのブログ](https://noimi.hatenablog.com/entry/2023/11/29/030313)でチャットアプリを使いチーム戦をするシーンがある．
問題文は数学的なモデルにしてから共有されていることがわかる．

　このように，問題文を数学的なモデルに言い換えてから問題を解くのは有用であると思う．
しかし，私はまだスムーズに数学的なモデルに置き換えられる訳ではないので練習していきたい．

## モチベーション

　競プロ精進のモチベーションを支えた要素を紹介する．

### ICPCチームメイト

　ICPCのチームメイトである二人が自分よりだいぶ先に青になっていたので，早く入青したい，追いつきたいという気持ちが強かった．
私は強くなりたいという感情より，負けているという負の感情の方が強くなれると知った．

|tenagazaru|soumat|
|:-:|:-:|
|<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">青色になりました！！！！嬉しすぎ！！！ <a href="https://t.co/5Su1qWphio">pic.twitter.com/5Su1qWphio</a></p>&mdash; テナガザル (@tenagazaru5) <a href="https://twitter.com/tenagazaru5/status/1749107266719215733?ref_src=twsrc%5Etfw">January 21, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>|<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">入青！！<br><br>soumatさんのAtCoder Beginner Contest 338での成績：186位<br>パフォーマンス：2206相当<br>レーティング：1575→1656 (+81) :)<br>Highestを更新し、2 級になりました！<a href="https://twitter.com/hashtag/AtCoder?src=hash&amp;ref_src=twsrc%5Etfw">#AtCoder</a> <a href="https://twitter.com/hashtag/ABC338?src=hash&amp;ref_src=twsrc%5Etfw">#ABC338</a> <a href="https://t.co/Fown9WdWI0">https://t.co/Fown9WdWI0</a></p>&mdash; ソウマット (@soumat_13) <a href="https://twitter.com/soumat_13/status/1751245520176300090?ref_src=twsrc%5Etfw">January 27, 2024</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>|

### K-POPアイドル

　水色の期間でK-POPにはまった．アイドルたちが私を応援してくれている（気がした）ため，頑張ることができた．
かわいいし格好いいしで最高．
ちなみに，韓国語は一ミリも理解していない．
私はK-POPアイドルのダンスパフォーマンス動画が好きだが，観客の歓声が入っており好みが分かれるところである．そ
のためここではおすすめ曲の動画を紹介することにとどめ，ダンスパフォーマンス動画の視聴は読者への課題とする．

|<iframe width="512" height="288" src="https://www.youtube.com/embed/pG6iaOMV46I?si=thxPvpOmSdCL0O8u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>|<iframe width="512" height="288" src="https://www.youtube.com/embed/dYRITmpFbJ4?si=mthbCQPrfFwuTdcA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>|
|:-:|:-:|
|<iframe width="512" height="288" src="https://www.youtube.com/embed/4vbDFu0PUew?si=U_2j39zyyvQJxG3b" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>|<iframe width="512" height="288" src="https://www.youtube.com/embed/Q3K0TOvTOno?si=ixkRci97Syp65Ksf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>|

### 煉獄杏寿郎

　８巻後半，煉獄杏寿郎が死に際に放つ「**君が足を止めてうずくまっても時間の流れは止まってくれない　共に寄り添って悲しんではくれない**」というセリフがお気に入り．
競プロっぽく言うと「コンテストでレートを溶かしてヘコんで立ち止まっている時間がもったいない」という感じだと思う．
レート下がってもあまりヘコまず頑張ろうと思わせてくれる．

## 最後に

　これからは青安定，そして入黄を目指して頑張る．
入灰→入水に960問，入水→入青に888問かかったことからあと2000問くらい解く必要がありそうだなと思っている．
気長にやっていきたい．
また，やはり自分の目標はICPCにあるから，ABCの問題だけでなくARC/AGCやCodeforces，ICPCの問題を積極的に解いていきたいと思う．

　ここまで長い文章を読んでいただきありがとうございました．
