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

中間に右向きと左向きの矢印を持つ線を描くためのもの. (矢印の位置調節可能)
```
%%%%% middle arrow %%%%%
\tikzset{
    ->-/.style={
        decoration={
            markings, mark=at position #1 with {
                \arrow[thick, black]{>}
            }
        }
    ,postaction={decorate}}
}

\tikzset{
    -<-/.style={
        decoration={
            markings,mark=at position #1 with {
                \arrow[thick, black]{<}
            }
        }
    ,postaction={decorate}
}
```
矢印以外にも arrow tips を参照して `->-` の真ん中を変えることでカスタムできます, 例えば,
```
\tikzset{
    -|-/.style={
        decoration={
            markings, mark=at position #1 with {
                \arrow[thick, black]{>}
            }
        }
    ,postaction={decorate}}
}
```
とすると, 中間に縦棒のある線が描けます.

---

間隔の狭い 2 本の並行した線を引きます. (正確には黒い太線の中心に白い細線を引いているのだと思います.)
あまり使う場面もないし, 頑張って並行してそうな 2 本の線を引けば問題ないので必要ないでしょう.
```
%%%% triple line %%%%%
\tikzset{
    triple/.style args={[#1] in [#2] in [#3]}{
        #1,preaction={preaction={draw,#3},draw,#2}
    }
}
```

## Examples

今後, 例などを書きながら説明していこうと思います. (続く)
