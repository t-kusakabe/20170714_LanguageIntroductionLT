# 言語紹介LT
# Ruby

---

## アジェンダ
- 特徴
- 面白いところ
- 自分がRubyを使う理由

---

# 特徴

---

### 全てのデータがオブジェクトである

>>>

- メソッドを持たない値がない
- 全てのデータはあるクラスのインスタンス

>>>

`#class` メソッド

- レシーバのclassを取得できる

```
irb(main):001:0> 'foo'.class
=> String
irb(main):002:0> nil.class
=> NilClass
```

>>>

### 演算もメソッド呼び出し

```
# Rubyの単純な演算
1 + 2
=> 3

# 本来はこう
1.+(2)
=> 3
```

>>>

### try method

レシーバに対して引数にシンボルで受け取ったメソッドが使えるのであれば実行、できなければnilを返す

```
require 'active_support'
require 'active_support/core_ext'

class Foo
  def self.bar
    puts 'this is bar method'
  end
end

Foo.bar
this is bar method
=> nil

Foo.barrrrrrrrrrrr
NoMethodError: undefined method `barrrrrrrrrr' for Foo:Class

Foo.try(:barrrrrrrrrrrr)
=> nil
```

>>>

おっと...？

>>>

Fooクラスにtryメソッドなんて定義していないはず。。。

>>>

書くsuperclassを調べて見ると。。。

```
Foo.class.superclass.superclass
=> Object

Foo.method(:try).class.superclass
=> Object
```

>>>

objectにたどり着く。

>>>

rubyのclassはどこかでobjectを継承している。<br>
基本的なmethodはKernel moduleで定義されていて、object classがKernel moduleをmixinすることで自作classに定義していないmethod等を使うことができる。

>>>

結論 : 他の言語と大体同じです

---

# 面白いところ

---

## ダックタイピング

ダック・タイピング（duck typing）とは、Smalltalk、Perl、Python、Rubyなどのいくつかの動的型付けオブジェクト指向プログラミング言語に特徴的な型付けの作法のことである。それらの言語ではオブジェクト（変数の値）に何ができるかはオブジェクトそのものが決定する。つまり、オブジェクトがあるインタフェースのすべてのメソッドを持っているならば、たとえそのクラスがそのインタフェースを宣言的に実装していなくとも、オブジェクトはそのインタフェースを実行時に実装しているとみなせる、ということである。

>>>

コードにして見ると。。。

```
def add(x, y)
  puts x + y
end

add(?, ?)
```

>>>

おそらくadd methodを作った人はこういう使い方を期待している

```
def add(x, y)
  puts x + y
end

add(1, 2)
3
=> nil
```

>>>

でも実際は。。。

```
def add(x, y)
  puts x + y
end

add('TECH', 'CAMP')
TECHCAMP
=> nil
```

>>>

文字列の連結をすることができる。

>>>

Javaだと...

```
public class Test {
  public static void main(String[] args) {
    add(1, 3);
  }

  public static void add(int x, int y) {
    System.out.println(x + y);
  }
}
```
letとかいう人うるさい。

>>>

- データとロジックが分離される。
- ロジックを変えることなくデータを変えることができる。

>>>

それでもやっぱり
- 型ないとか怖い
- 信用できない

>>>

Ruby3で型に関する実装がされるみたい<br>
気になる人はRuby Kaigi2016のmatzのレポートみてください

---

# 自分がRubyを使う理由

---

- 自由度高い
- 簡単にちゃちゃっとscript書ける
- 自分の周りでRubyの需要が多い

---

## 自由度に関して

>>>

rubyの基本の書き方

```
Kernel.puts('Happy Hacking')
Happy Hacking
=> nil
```

>>>

rubyはスペース挟むと引数をとる

```
Kernel.puts 'Happy Hacking'
Happy Hacking
=> nil
```

>>>

頑張れば `.` も消せる

```
code = "
Kernel　puts 'Happy Hacking'
"

eval(code.gsub(/　/, '.')
Happy Hacking
=> nil
```

>>>

(´・ω・｀) oya?

>>>

おわかりいただけただろうか？

>>>

アセンブリ言語(CASL)

```
MSG DC 'Happy Hacking'
```

>>>

２つを並べてみると...

```
Kernel　puts 'Happy Hacking'  # 一部抜粋

MSG DC 'Happy Hacking'
```

>>>

(｀・ω・´)似てる！

>>>

ずっとこれがやりたかった！！！
![](pic/pic1.png)

>>>

ただ時間がなかったのでできてません。。。

>>>

このLTでRubyに興味を持ってくれた方！

>>>

是非ともRubyでfizzbuzzしてみてください。

>>>

CASL嫌いな1年生はとりあえずRubyしてみよう！

>>>

割とがちで作って欲しいのでチケット立ててます

![](pic/pic2.png)

>>>

みなさんPR待ってます♡

---

## *~ fin ~*
![](pic/pic3.png)
