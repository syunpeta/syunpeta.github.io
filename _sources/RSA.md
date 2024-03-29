---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---





# RSA暗号

## フェルマーの小定理
$p$が素数のとき、$\mathbf{Z}_p^*=\{1,2,...,p-1\}$である。  
任意の$a \in \mathbf{Z}_p^*$に対して

$$
a^{p-1} = 1 \pmod{p}
$$

が成り立つ。



## ポーリック-ヘルマン暗号

以下のような共通鍵暗号方式を**ポーリック-ヘルマン暗号方式**という。

- 鍵生成

1. 入力$1^n=1...1$ に対して$n$ビットの素数$p$をランダムに生成する。
2. $gcd(e,p-1)=1$となる$e$をランダムに選ぶ。
3. 拡張ユークリッドの互除法を用いて$ed = 1 \pmod{p-1}$となる$d>0$を求める
4. 秘密鍵を$(p,e,d)$とする。

- 暗号化  

平文$m \in \mathbf{Z_p}^*$に対し、暗号文$c$を

$$
c = m^e \pmod{p}

$$

とする。

- 復号化  

暗号文$c \in \mathbf{Z}_p^*$に対し平文$m$を

$$
m = c^d \pmod{p}
$$

と求める。

この復号化手順は以下のように正当性を確かめることが出来る。

鍵生成手順の3番目の式、$ed = 1 \pmod{p-1}$より、任意の整数を$r$とすると

$$
ed = 1 + r(p-1)

$$
と書くことが出来る。復号化手順とフェルマーの小定理より

$$
\begin{equation}
\nonumber
\begin{aligned}
c^d &= (m^e)^d \pmod{p}\\
&= m^{ed} \pmod{p}\\
&=m^{1+r(p-1)}\pmod{p}\\
&=m(m^{p-1})^r\pmod{p}\\
&=m \pmod{p}
\end{aligned}
\end{equation}

$$

これより復号化の正当性が確認できた。  
この暗号は共通鍵暗号方式なので鍵の公開は行わない。しかし、もし$(e,p)$を公開出来たら公開鍵暗号方式として機能しそうである。ただし、今のままだと拡張ユークリッドの互除法を用いると誰でも簡単に秘密鍵$d$を計算できてしまうので、何らかの工夫が必要である。

--- 

## RSA暗号
RSA暗号はポーリック-ヘルマン暗号の素数$p$を合成数$N=pq$に置き換えたものである。
もし、$p,q$が$3,7$など小さい数である場合は$N=21$から簡単に$p,q$を素因数分解することが出来てしまうが、巨大な素数の組である場合は$N$から$p,q$を計算することは難しい。これによって合成数$N$を公開鍵として公開しても、秘密鍵を計算することが難しい仕組みを作ることが出来る。  
RSA暗号のアルゴリズムは以下のようになる。

- 鍵生成
1. 入力$1^n$に対し、$n$ビットの素数の組$(p,q)$をランダムに生成し$N=pq$とする。
2. $gcd(e,(p-1)(q-1)) = 1$となる$e$をランダムに選ぶ
3. 拡張ユークリッドの互除法を用いて$ed=1 \mod(p-1)(q-1)$となる$d>0$を求める。
4. 公開鍵を$(N,e)$、秘密鍵を$d$とする。

- 暗号化  
公開鍵$(N,e)$と平文$m\in \mathbf{Z}_n^*$から暗号文$c$を

$$
c = m^e \pmod{N}
$$

とする。

- 復号化  
秘密鍵$d$と暗号文$c\in \mathbf{Z}_N^*$から平文$m$を

$$
m = c^d \pmod{N}
$$
と計算する。

## オイラー関数とオイラーの定理
RSAの復号の正当性を解説する前に、オイラーの定理を紹介したい。  
### オイラーの定理
$n$を正の整数、$a$を$n$と互いに素な正の整数とする。このとき、

$$
a^{\phi(n)} = 1 \pmod{n}
$$

が成立する。これを**オイラーの定理**と呼ぶ。  
この定理はフェルマーの小定理を合成数$n$に拡張したものである。  
この定理で使われる$\phi(n)$を**オイラー関数**と呼ぶ。

### オイラー関数
オイラー関数は正整数$n$に対して1から$n$までの整数のうち$n$と互いに素なものの個数を返す関数である。例えば$n=9$とすると、$\phi(9) = \#\{1,2,4,5,7,8\}=6$となる。  
$n$が素数の場合、1から$n-1$までの整数は全て互いに素になるため$\phi(n)=n-1$となる。  
また、互いに素な自然数$k,l$が存在したとき、$\phi(kl) = \phi(k)\phi(l)$となる。

実際にオイラー関数を計算してくれる[サイト](https://keisan.casio.jp/exec/user/1511790555)もあるので適当な数字で遊んでみると面白い。

## RSA復号の正当性
ポーリック-ヘルマン暗号と同じように確認することが出来る。

$$
\begin{equation}
\nonumber
\begin{aligned}
c^d &= (m^e)^d\pmod{N}\\
&= m^{1+r(p-1)(q-1)} \pmod{N}\\
\end{aligned}
\end{equation}
$$

ここで、$p,q$は素数であり、当たり前だが互いに素なので$\phi(N) =\phi(p)\phi(q)= (p-1)(q-1)$より

$$
\begin{equation}
\nonumber
\begin{aligned}
m^{1+r(p-1)(q-1)} \pmod{N} &= m^{1+r\phi(N)} \pmod{N}\\
&=m(m^{\phi(N)})^r\pmod{N}\\
&=m\pmod{N}
\end{aligned}
\end{equation}
$$

となり復号の正当性が確認できた。


## RSA実装
分かりやすさ重視のため一部冗長な表現をしている部分もある。より高速化をするにはべき乗剰余をMontgomery乗算や並列化するなどが考えられる。  
$n$ビットの素数$p,q$をランダムに生成する際はPycryptodomeという暗号ライブラリを用いている。実行の際は先に

```Python
pip install pycryptodome
```

でインストールをする必要がある。  

pythonによるRSAの実装例を以下に示す。

```{code-cell}
from Crypto.Util import number
from random import randint,getrandbits
import math

class RSA:
  def __init__(self,n):
    #security bit n
    self.n = n
  
  #Extended Euclid Algorithm
  def Ex_Euclid(self,a,b):
    if b == 0:
      return 1,0,a
    else:
      q = a//b
      r = a%b
      s,t,c = self.Ex_Euclid(b,r)
      x = t
      y = s-q*t
      return x,y,c


  def keygen(self):
    self.p = number.getPrime(self.n)
    self.q = number.getPrime(self.n)
    self.phi_N = (self.p-1)*(self.q-1)
    self.N = self.p*self.q

    #generate e gcd(e,N)=1
    e = randint(2,self.phi_N-1)
    while math.gcd(e,self.phi_N) !=1:
      e = randint(2,self.phi_N-1)
    
    #compute modular_inverse d 
    _,d,__ = self.Ex_Euclid(self.phi_N,e)

    #secret_key
    self.d = d%self.phi_N
    #public_key
    self.e = e
  
  def enc(self,m):
    return pow(m,self.e,self.N)
  
  def dec(self,c):
    return pow(c,self.d,self.N)

  def get_keys(self):
    return self.e,self.d,self.p,self.q,self.N
  
#security bit
k=128
rsa = RSA(k)
plain_txt = getrandbits(k)
rsa.keygen()
enc_plaintxt = rsa.enc(plain_txt)
dec_plaintxt = rsa.dec(enc_plaintxt)
e,d,p,q,N = rsa.get_keys()


print("plaintext is :",plain_txt)
print("Prime number p,q,N :",p,q,N)
print("public key e :",e)
print("secret key d :",d)
print("encrypted plain_text :",enc_plaintxt)
print("decrypted encrypted_text :",dec_plaintxt)

```





