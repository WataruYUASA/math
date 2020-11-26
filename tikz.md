---
layout: page
title: TikZ tips
permalink: /tikz/
---

ここでは自分が結び目関連の論文で使っている TikZ 環境と例を挙げます.
できるだけ複雑なライブラリは使わずに, 描画コマンドも簡単なものしか使用しないようにしています.
あまり詳しいことはわからないので, 正しくない記述であったり, 各々の環境によって調節が必要かもしれませんが自分用のメモも兼ねて書いておきます.  
たぶん TikZ はインストールされてるかと思います. 
わからない事があればインターネットで検索したり, [膨大な TikZ manual](https://github.com/pgf-tikz/pgf) を読めば解決すると思います.

## Preamble

プリアンブルには以下を記入 :

``` 
\usepackage{tikz}  
\usetikzlibrary{calc,decorations.markings}  
\usetikzlibrary{arrows.meta}
```

## Document

` \begin{document} ` の直後に以下を記述します.
まずは準備です.
後で, 使い方を説明します.

---

中間に右向きと左向きの矢印を持つ線を描くためのもの. 矢印の位置, 色が調節可能. デフォルトは真ん中 (0.5) にベースの色で矢印が描かれる.

```arrow
\tikzset{->-/.style 2 args={
    postaction={decorate},
    decoration={markings, mark=at position #1 with {\arrow[thick, #2]{>}}}
    },
    ->-/.default={0.5}{}
}

\tikzset{-<-/.style 2 args={
    postaction={decorate},
    decoration={markings, mark=at position #1 with {\arrow[thick, #2]{<}}}
    },
    -<-/.default={0.5}{}
}
```

例えば,

```
\draw[blue, ->-={.9}{red}] (0,0) -- (1,0);
```

とすると, blue の線の 0.9 の位置に red で矢印が描かれる.

矢印以外にも arrow tips を参照して `\arrow[thick, #2]{<}` の部分を変えることでカスタムできます.

---

間隔の狭い 2 本の並行した線を引きます. (正確には黒い太線の中心に白い細線を引いているのだと思います.)
あまり使う場面もないし, 頑張って並行してそうな 2 本の線を引けば問題ないので必要ないでしょう.

```triple_line
\tikzset{
    triple/.style args={[#1] in [#2] in [#3]}{
        #1,preaction={preaction={draw,#3},draw,#2}
    }
}
```

---

結び目の絵を描く上で重要な上下のある交差を持つ線を描くために, 上を通る線を描きます.

```overarc
\tikzset{
    overarc/.style={
        white, double=red, double distance=1.2pt, line width=2.4pt
    }
}
```
例えば,

```
\draw (0,0) -- (2,2);
\draw[overarc] (0,2) -- (2,0);
```

とすると, 交差する線が描けると思います.
`overarc` は太い白線の中心に黒い線を描く事によって黒い線の両脇にスペースを作って, 上を通る線を描いています. なので, 上を通る線は後に描かないと意味がありません. (全て `overarc` を付ければ問題ないですが)

## Examples

今後, 例などを書きながら説明していこうと思います. (続く)
