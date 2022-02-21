---
layout: post
title: 確率変数と確率分布【統計学】
gh-repo: daattali/beautiful-jekyll
tags: [統計学]
comments: true
---
<script async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" id="MathJax-script"></script>
このページでは確率変数と確率分布について説明します。

## 確率変数
2つのさいころを投げた時出た目の和をXと置くと、Xとその出現確率は以下のようになります。  
  
| X | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |  
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |  
| 確率 | 1/36 | 2/36 | 3/36 | 4/36 | 5/36 | 6/36 | 5/36 | 4/36 | 3/36 | 2/36 | 1/36 |
  

このように値に対して確率が対応する変数のことを<span style="color: red; ">確率変数</span>と言う。  
特に今回の場合、Xが2,3,...,12と飛び飛び(離散値)になっている。  
このような確率変数を離散型確率変数と言い、逆に連続である確率変数のことを連続型確率変数という。  


## 確率分布
Xの取り得る値をx<sub>1</sub>,x<sub>2</sub>...,x<sub>n</sub>、その確率をp<sub>1</sub>,p<sub>2</sub>,...,p<sub>n</sub>とすると、

$$
\begin{align*}
P(X=x_{k}) = f(x_{k})= p_{k}    (k=1,2,...n)
\end{align*}
$$

のようにそれぞれの値の確率を表すことができ、このf(x)を<span style ="color: red">確率分布</span>という。  
例えば、上のさいころの例だと、f(2) = 1/36のようになる。  
Xが離散型確率変数であるとき、その確率分布を離散型確率分布といい以下のような条件を満たす。

$$
\begin{align*}
f(x_{k}) \geq 0 \quad (k=0,1,2...) \quad かつ \quad \sum_{k=1}^{\infty}f(x_{k})=1
\end{align*}
$$

また、Xが連続型確率変数であるとき、以下のように確率変数のとる値を定義することができる。

$$
\begin{align*}
P(a \leq X\leq b) = \int_{a}^{b}f(x)dx 
\end{align*}
$$

この時、以下の条件を満たす関数を連続型確率分布という。　　

$$
\begin{align*}
f(x) \geq 0 \quad かつ \quad \int_{-\infty}^{\infty} f(x)dx =1
\end{align*}
$$