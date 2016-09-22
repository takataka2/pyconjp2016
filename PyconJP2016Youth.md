# PyconJP2016 Youth

# はじめに
Youth Corder Workshopへようこそ。このワークショップではみなさんにPython（パイソン）というプログラミング言語を使ってネットから自動で情報を集めてきたり、集めた情報を地図に表示させたり扠せたりといった体験をしてもらいます。これらの体験からPython（パイソン）の便利さ、楽しさを感じ取ってもらうことがこのワークショップの目的です。

## そもそもPython（パイソン）ってなに？
Pythonはたくさんあるプログラミング言語のひとつです。プログラミング言語はコンピュータに命令して、自分の思うとおりに仕事をしてもらうためのことばと思ってください。

Pythonには次のような特徴があります。
 - 文法が簡単で覚えやすく、プログラムがシンプルに書ける。
 - 広い分野で優れたライブラリがある。


 またTIOBEという会社があるプログラム言語がどのくらい話題になっているかという基準でランキングを発表しています。そのランキングによればPythonは５位で、非常に注目されている言語だといえます。

 [リンク: TIOBEプログラムランキング](http://www.tiobe.com/tiobe-index/)

# Pythonを使ってみる
さっそくpythonを使ってみましょう。パソコンのデスクトップにある***「WinPython-32bit-3.4.4Qt5」***というアイコンをダブルクリックしてみてください。今回のワークショップではこのフォルダのみ使用します。

## Spiderを起動する
Pythonのプログラムを書く方法はいくつかありますが、今回は***「Spyder」***というツールを使います。フォルダ内の「spyder.exe」というファイルをダブルクリックしてください。下のようなウインドウが出ると思います。

<img src=https://github.com/takataka2/pyconjp2016/blob/master/img/spider.PNG?raw=true width=640x>

画面の左側にプログラムを書きます。そして画面の右下に実行結果が表示されます。

## Pythonの書き方
ここからは実際にプログラムを書きなながら、Pythonを使っていきます。

### 文字を表示する
まず最初は文字を表示するプログラムです。pythonでも字を表示するときはprint関数を使います。関数というのはよく使うプログラムを一つにまとめたものと思ってください。

注意点としては文字列は```""```(ダブルクォーテーション)
または```''```（クォーテーション）でくくる必要があります。

```
print("こんにちは")
```

## 計算する
今度は計算してみましょう。数字と足し算や掛け算の記号を組み合わせればよいだけです。

注意点としては掛け算は```*```(アスタリスク)
、割り算は```/```（スラッシュ）を使う必要があります。

```
print(1+2*3)
```

## 変数を使う
変数というのは数値や文字のデータにわかりやすいラベルをつけることです。あるデータに変数をつけるときは```=```で結びます。例えば次のようになります。

```
a = 1
b = 2
print(a+b)
```

文字列の場合はどうなるでしょう。やってみましょう。

```
a = "わはは"
b = "ガハハ"
print(a+b)
```

文字を足した場合は連結になります。

## リストを使ってみる
リストは複数のデータをまとめたものです。次のように使います。

```
list1 = [1,2,3,4]

print(list1[0])
print(list1[1])
print(list1[2])
print(list1[3])
```

## 繰り返しを使う
コンピュータのいいところは仕事をしても疲れないことです。とくに人間がうんざりするような繰り返しでも平気です。pythonで繰り返しは以下のようにやります。

```
for i in range(5):
    print("こんにちは")
```

実はiには0から4までの数字が順番に入っていきます。確かめてみましょう。

```
for i in range(5):
    print(i)
```

range(5)はリストで置き換えることが可能です。

```
for i in ["東","西","南","北"]:
    print(i)
```



## モジュールを使ってみる
Pythonでは他の人が作った便利なプログラムを使うことができます。このようなプログラムを***モジュール***と言います。他のプログラミング言語では***ライブラリ***と呼ばれることもあります。ここでは画像処理用のモジュールであるPILを使ってみます。


```
from PIL import Image

image = Image.open("tento_face150.png")
image.show()
```

## アスキーアートを作ってみる
いままで文法を使ってアスキーアートを作ってみます。以下のプログラムをコピーして、pyconjp2016のフォルダに保存してください。

```
# -*- coding: utf-8 -*-
"""
Created on Tue Sep 13 16:04:49 2016

@author: taka2
"""

'''
ASCII Art maker
Creates an ascii art image from an arbitrary image
Created on 7 Sep 2009

@author: Steven Kay
'''

from PIL import Image
import random
from bisect import bisect

# greyscale.. the following strings represent
# 7 tonal ranges, from lighter to darker.
# for a given pixel tonal level, choose a character
# at random from that range.

greyscale = [
            " ",
            " ",
            ".,-",
            "_ivc=!/|\\~",
            "gjez2]/(YL)t[+T7Vf",
            "mdK4ZGbNDXY5P*Q",
            "W8KMA",
            "#%$"
            ]

# using the bisect class to put luminosity values
# in various ranges.
# these are the luminosity cut-off points for each
# of the 7 tonal levels. At the moment, these are 7 bands
# of even width, but they could be changed to boost
# contrast or change gamma, for example.

zonebounds=[36,72,108,144,180,216,252]

# open image and resize
# experiment with aspect ratios according to font

im=Image.open("tento_face150.png")
im=im.resize((100, 100),Image.BILINEAR)
im=im.convert("L") # convert to mono

# now, work our way over the pixels
# build up str

str=""
for y in range(0,im.size[1]):
    for x in range(0,im.size[0]):
        lum=255-im.getpixel((x,y))
        row=bisect(zonebounds,lum)
        possibles=greyscale[row]
        str=str+possibles[random.randint(0,len(possibles)-1)]
    str=str+"\n"

print(str)
```
# インターネットとHTML
## インターネットの仕組み
　インターネットはもともとコンピュータネットワーク同士を結んだもの意味していました。しかしアメリカやヨーロッパを中心にネットワークをつなげているうちに超巨大なネットワークになってしまいました。現在はその巨大ネットーワークを「インターネット」と呼ぶことが多いと思います。


[リンク: インターネットの仕組み](http://www.soumu.go.jp/main_sosiki/joho_tsusin/security/basic/service/02.html)

## Webの基本はHTML
みなさんインターネットを使ってYahooやYoutubeなどのサイトをサイトを使っていると思います。サイトの表示には「HTML」という言語を使います。実際のサイトで確かめてみましょう。

[リンク: Yahoo Japan](http://www.yahoo.co.jp/)

マウスを右クリックして「ページのソースを表示」を選んでください。サイトの実際の内容が見てとてます。

ちょっとしたいたずらをしてみましょう。個別の文章を選んで右クリックで検証を選びます。

## ホームページを作ってみる
我々も簡単なホームページを作ってみましょう。次のように打ち込んだ後、```test.html```で保存してください。この形がHTML文章の最も基本的な話になります。

```test.html
<html>
  <head>
    ここに各種設定が入る
  </head>

  <body>
  　ここに本文が入る
  </body>
</html>
```
## 見出しをつける
文字列を```<h1> </h1>```で囲うと見出しになります。数字を大きくすると文字はだんだん小さくなります。

```test.html
<html>
  <head>
    ここに各種設定が入る
  </head>

  <body>
  　<h1>タイトル</h1>
  　<h2>章</h2>
  　<h3>補足</h3>
  　
  </body>
</html>
```

## リンクを付ける
指定したページに飛んで行くためのリンクは***<a>***タグを使います。

```test.html
<html>
  <head>
    ここに各種設定が入る
  </head>

  <body>
  　<a href="https://www.google.co.jp"/>ここをクリック！</a>
  </body>
</html>
```

## 画像を表示する。
画像を表示するときは<img>タグを使います。以下のようにします。

```test.html
<html>
  <head>
    
  </head>
  <body>
  　<img src="pica.jpg"/>
  </body>
</html>
```


# Google Mapを使う
## 地図データが熱い!!
最近世界中で自動運転の研究が盛んです。世界中の自動車メーカーが自動運転車の開発に取り組んでいますが、現在はGoogleが一歩先に行っているようです。2012年ごろからテストが始まり、最近まで190万キロメートル走っても無事故でした。（残念ながら2016年２月にバスと接触事故を起こしています。）

|グーグルカー|
|---|
|<img src=https://github.com/takataka2/pyconjp2016/blob/master/img/prototype-early.jpg?raw=true width=320px)>|

また最近話題になったゲームに「ポケモン Go」があります。実際の町中でポケポンを捕まえるこのゲームは世界中で人気になりました。

|ポケモンGO|
|---|
|<img src=https://github.com/takataka2/pyconjp2016/blob/master/img/pokemon_go_soft_launch.jpg?raw=true width=320x>|

「自動運転」と「ポケモンGo」にはひとつ共通点があります。それは地図データを多用しているということです。とくにスマートフォンが普及してからはアプリやウェブ使って手元で地図を利用できるようになりました。このワークショップでは「Google Map」を題材にして、もっと自在に地図データで遊ぶことを目的にしています。


## Google Mapをまず表示してみる。
まずGoogle Mapを表示させてみます。なお詳細なレファレンスは下記のリンクあります。

[グーグル・マップレファレンス](https://developers.google.com/maps/documentation/javascript/tutorial?hl=ja)


```
<html lang="ja">
    <head>
        <meta charset="utf-8">
        <title>Google Map</title>
        <script src="http://maps.google.com/maps/api/js?sensor=true&language=ja"></script>
        <style>
            #map {
                width: 100%;
                height:100%;
            }
        </style>
    </head>
    <body>
        <div id="map"></div>
        <script>
            var latlng = new google.maps.LatLng(35.66,139.69);
            var options ={
                zoom: 15,
                center: latlng,
                //navigationControl: false,
                mapTypeId: google.maps.MapTypeId.ROADMAP
            } 
            var map = new google.maps.Map(document.getElementById("map"),options)
         
                                
        </script>
    </body>
</html>
```

