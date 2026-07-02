---
layout: post
title: powershell-パイプでGo！
date: 2026-06-07 10:00:00 +0900
last_modified_at: 2026-07-02 10:00:00 +0900
categories: scripts
---

<h2> powershell？ナニソレ？ 美味しいの？</h2>


<H4> --- 目次 --- </H4>
* ここにtoc表示
{:toc}

### **powershell** とは？・・ (260607)

 - windowsについてるターミナルとかいう黒い画面でゴニョゴニョ呪文を書いてコンピュータを動かすソフト
 - wikipediaを参照しても良いけど語り口が熱くないので[こちら](https://udemy.benesse.co.jp/business/efficiency/powershell.html)がアウトラインを知るにはおススメ
  - まずは見てみよう
  1. windowsのスタートメニューをクリック
  1. 上部の検索窓に power と入れると Windows PowerShell 開くと出るのでクリック  
  <img src="/assets/img/powershell1st.png" alt="sh1" width="480">  
     こんなのが出ればとりあえずOK!
  1. コマンド(=命令)を入れて実行してみよう
  1. 半角文字でpsと入れてenterキーを押すと・・・
  1. ズラズラッと文字が流れて出てきたよね？意味わかんないよね？
  1. ここでマウスホールをころころ回すと画面をさかのぼって見ることができます。でもそれだけ・・・
  1. ん、じゃ命令、コマンドっていうか正確にはコマンドレットって言うらしい  
    大して重要でもないけどAIに尋ねるときやググるときに出やすくなるので一応記憶！
  1. ここでキーボードの **↑**キーを押すとあら不思議、先ほどのコマンドレットが出てきました。
  1. で、この後ろにパイプ記号を追加します。キーボード右上のほうの¥記号のキーをshiftキーを押しながら押すと ｜ 縦棒の記号が現れる！これがパイプです。この記事ではこのパイプの利用のメリットや使い方にフォーカスして話を進めます。
  1. で、今打ち込んだパイプ記号の後ろに ogvと半角で打ち込んでenterを押してみて！  
  <img src="/assets/img/pipe1st.png" alt="pp1" width="200">  
  1. こんなの出た？  
  <img src="/assets/img/ogv1st.png" alt="og1" width="640">
  1. ちょっとだけ解説すると最初に入れた **ps** はGet-Processの略で現在実行中のwindowsの裏とかで動いてるサービスやプログラムの状態を教えてくれる。後から入れた **ogv** はOut-Gridviewの略でパイプでつないだ前の命令の結果をexcelみたいなグラフィカルな形式で表示してくれるコマンドレット。
  1. で、表示されたogvの窓の中で項目をクリックすると並び替えとかもしてくれる。  
  例えばCPUってとこをクリックしてやればパワーをたくさん使ってる順やあまりパワーを食って無い順にしてプロセスを見ることができるって訳。  
  **ps｜ogv** ってパイプ入れて6文字だよ、凄くね。
  1. ちなみにコマンドレットでよく使われるものは今回みたいにaliasという略称・別名が設定されている。どんなものがあるかはpowershellにaliasといれればリストが得られます。
  1. さて今回はどうでした！　次回はもう少し環境と応用の探し方の話を書きますね。こうご期待！！
   
### パイプでどんなふうにpowershellを働かせるのかな？・・ (260609)

 - この間のps｜ogvを振り返ってみましょう。  
ps というコマンドレット(命令)とogvって言うのをパイプ(｜)でつないでましたね。
 - このpsは正式にはGet-Processで現在windowsの中で稼働しているプロセス(裏方含めたプログラム)を列挙してくれる命令です。このようにpowershellには現在のPCの様々な情報を得るための命令がたくさん入ってます。　
 - 黒い画面で Get-Command Get*と入れてenterするとずらずらっと出てきます。はっきり言って多すぎて困るくらいです。でも我々にはAIという強い見方がいるのでchatGptとかで「powershellのget-xxxってコマンドレットで初心者が使うと便利なのは？」なんて聞くと  

まず毎日使う5選  
 - ファイル一覧　Get-ChildItem  または gci  または ls  
  gci *.xlsx  
  gci -Recurse *.fsx  
 - ファイルを見る。 Get-Content  
   Get-Content test.txt または gc test.txt
     - ログ監視なら  
     gc log.txt -Wait　・・ Linuxのtail -f みたいなもの  
     ・  
     ・  
     ・  

のように長ーい文章を惜しげもなく出してくれます。当然知らないことも多いのでちょっと気になった文をコピペして　これは？？みたいに聞くといくらでも深堀り出来ます。  
んでもってこの後ろに ｜ogvってつけてやれば大好きなexcelもどき画面で出てきた結果をいくらでも眺めることができます。

 - それだけじゃ、発展が無いって？じゃちょっと進めますね。  
   ps ｜ Select-Object Name, Id, WS, CPU ｜ ogv  
   こうするとプロセスの名前と同じ名前の時に見分けるIDとメモリーの食い方を見るWSとCPUの消費量を見るCPUだけになりました。  
   タイトル部分のクリックでどのプロセスが消費しているのかわかりますね。余計な情報も無くて見やすい

 - これをさらに次のように書き変えると  
   ps ｜ Select-Object Name, Id, WS, CPU ｜ ogv -passthru  
   あれ？変わってない？と思います？   
   ctrlキーを押しながら適当な行をいくつかマウスで左クリックしてenter押すと
```  
Name                    Id       WS CPU  
----                    --       -- ---  
AggregatorHost        7232 22872064  
ApplicationFrameHost 15556 43966464 0.25  
AutoHotkey64         13364 14151680 1.38  
CrossDeviceResume     9072 55586816 0.62
```  

  みたいなのが現れませんか！つまり任意の選択した行を出力できるんです。  そしてこれをさらにパイプでつないで次の処理を行うことができますね。 
  すぐに思いつくのはexcelへの出力、次はpowershellでexcelを取り込んだり出力したりすることを説明します。

### excel入出力を出来るようにする ・・ (260611)

まずはpowershellをターミナルで起動してください。  
そこで  
```
Install-Module -Name ImportExcel -Scope CurrentUser -Force
```
と打ち込んでください。
モジュール名は ImportExcelって言うみたいですね。  
1分も経たないうちに終わったみたい。  

```
Get-Module -ListAvailable ImportExcel
```
と入れてみてこんな風な出力がでたらOK！
```
ModuleType Version    PreRelease Name                                PSEdition ExportedCommands
---------- -------    ---------- ----                                --------- ----------------
Script     7.8.10                ImportExcel                         Desk      {Add-ConditionalFormatting, Add-ExcelCh…
```
さっそく使ってみましょう
ImportExcelモジュールは外部のexcelの読み込みにも出力にも使えますがまだ読むべきexcelファイルが現在のフォルダに無いと思いますのでちょっと作ってみましょう。

```
$data = @(
    [pscustomobject]@{ Name = "Alice"; Score = 90 }
    [pscustomobject]@{ Name = "Bob";   Score = 75 }
)

$data | Export-Excel test.xlsx -AutoSize
```
ちょっと長いですが上記のように打ち込めば  
test.xlsxが作成されます。上下を2回に分けて入力してもok!   
ls と入れてenterでフォルダ内のファイルリストがずらずらと出ますがtest.xlsxがあれば大成功！  
ここで start test.xlsxとしてやれば出来立てのexcelファイルが開きます。  
次回は別のexcelファイルを読んで加工するスクリプトを作ってみましょう。

### 今、どうしてpowershellに注目するのか？ ・・ (260702)

会社のPCなどで自動化のために何かのフリーの言語(pythonなど)を入れたくても自由に入れられない会社も増えてます。その点、powershellならwindowsに最初から入ってます。  
（少なくともwindows11であればpowershell 5.1は）  
そして外部ソフトインストール禁止の会社でもzip配布のpwsh.exe(7.xx)ならすぐにも使えるんですよ。  

この7.xx系と5.1の関係は割と複雑な事情があって今、本流は7.xx(実行ファイル名 pwsh.exe)なんだけどwindowsにプリインストールされてるのは5.1(実行ファイル名 powershell.exe)でほとんど同じ動きをするんだけどpwshはオープンソースのソフトでmacやlinux系でも動く、でもpowershellはwindowsオンリー

自分はpwshベースでいろいろな実験・開発を楽しんでいる。  
もしも紹介しているソースが変な動きをしたりしたらトップページのコメントから教えていただけると嬉しいです。

ともあれwindowsに入っているってことですぐに使い始めることは可能ってことです。  
で、powershellのお勧めの理由ですが  
 - コマンドレットと呼ばれるwindowsの種々の管理用の部品が最初から用意されている  
   これによってプロセスのコントロールや大量のファイルの整理などが簡単にできたりグラフィッカルな表のフォームを1行で表示したりも出来ます。
 - コマンドレットなどを1行実行すると結果は目に見える形で開発する画面の中ですぐに見ることができる。まあpythonとかのreplと呼ばれる機能と同じですね。
 - コマンドレットの出力を次のコマンドレットに渡すためにパイプと呼ばれる記号でつないで記述できる  
   つまり部品１つでする処理を小さくしてそれをパイプでつないで開発をすることができるんです。  
   これは１つのプロセスで行う処理が小さい上に最初から用意されている専用のコマンドレットがあるので項目を絞ったり、条件で次の段に流すデータに制限を加えたりして開発を進めることができます。
 - 最初の入力部分のための専用の部品があり、excel,csv,database,jsonなど各種のデータを一元化して処理できます。
 - 出力段も充実していてexcel,csv,テキストいろいろ行けます。

今後、このページでももっと例を挙げていきたいと思いますが  
「プログラムって難しいんでしょ！」って言われる方にもぜひ使っていただきたい便利なツールなのでそのあたりも含め乞うご期待！

### Geminiにちょっとした入門記事を作ってもらったよ！ ・・ (260702)

PowerShell（pwsh）の世界へようこそ！  
このテキストは、PowerShellの「一番おいしいところ」であるデータの読み込み・加工・出力（パイプライン処理）を、初心者でも手を動かしながら楽しく学べるロードマップです。

難解なプログラムの文法は後回しにして、まずは「コマンドをつなぐだけで仕事が終わる快感」を体験しましょう！

📄 1: PowerShellって何？＆ 魔法の土台
PowerShellは、Windows/Mac/Linuxで動く強力な自動化ツールです。
最大の特徴は、すべてのデータが「文字（テキスト）」ではなく、「オブジェクト（データの塊）」として流れる点です。

まずはPowerShellを起動し、最も重要な「動詞-名詞」のルールと、コマンドを探すコマンドを覚えましょう。

PowerShell
 1. 現在の場所（ディレクトリ）のファイル一覧を見る
Get-ChildItem

 2. コマンドを探す（「CSV」に関係するコマンドを見つける）
Get-Command *Csv*
💡 コラム：コマンドレット（Cmdlet）とは？
PowerShellのコマンドは「Get-ChildItem」のように「動詞-名詞」の形をしています。これをコマンドレットと呼びます。

📄 2: データの入力① 〜最強のデータ形式「JSON」〜
現代のITで最もよく使われるデータ形式がJSON（ジェイソン）です。
PowerShellなら、インターネット上のデータやJSONファイルを、1行で「中身を自由に扱えるデータ」に変換できます。

JSONファイルを読み込む
まずは、デスクトップなどに member.json というファイルを作ってみましょう（文字コードはUTF-8）。

```JSON
[
  {"Name": "Alice", "Age": 25, "Role": "Developer"},
  {"Name": "Bob", "Age": 30, "Role": "Designer"},
  {"Name": "Charlie", "Age": 22, "Role": "Developer"}
]
```
これをPowerShellで読み込みます。

```PowerShell
# JSONを読み込んで自動で「データ（オブジェクト）」に変換
$users = Get-Content ./member.json | ConvertFrom-Json

# 画面に表示してみる
$users
```

📄 3: データの入力② 〜ビジネスの王道「CSV」〜
ExcelでもおなじみのCSVファイル。PowerShellはCSVの処理が超得意です。
先ほどのメンバーリストをCSV（member.csv）にしたと仮定して、読み込んでみましょう。

```Plaintext
Name,Age,Role
Alice,25,Developer
Bob,30,Designer
Charlie,22,Developer
```

CSVファイルを読み込む
```PowerShell
# CSVを読み込む（Shift-JISの場合は -Encoding Default をつける）
$csvData = Import-Csv ./member.csv

# 読み込んだ中身を確認
$csvData
```
これだけで、ただのカンマ区切りのテキストが、PowerShell内で扱える綺麗なテーブルデータになります。

📄 4: データの入力③ 〜みんな大好き「Excel」〜
実は、標準のPowerShellはExcelを直接読めません。しかし、世界中で使われている「ImportExcel」という拡張機能（モジュール）を入れれば、Excelアプリが入っていなくても爆速で読み書きできます！

魔法の準備（最初の一回だけ）
```PowerShell
# Excelを扱うための拡張機能をインストール（確認画面が出たら「Y」）
Install-Module ImportExcel -Scope CurrentUser
Excelファイルを読み込む
member.xlsx というExcelファイル（シート名は「Sheet1」）があるとします。
```

```PowerShell
# Excelを1行で読み込む！
$excelData = Import-Excel ./member.xlsx -WorksheetName "Sheet1"

$excelData
```

📄 5: パイプライン（|）という革命
PowerShellの一番の楽しさはパイプライン（|）にあります。
パイプラインとは、「左側のコマンドの実行結果を、右側のコマンドにそのまま引き渡す」仕組みです。

バケツリレーをイメージしてください。

Import-Csv がデータを1件ずつ取り出す

パイプ | を通って次のコマンドへ流す

次のコマンドがそれを加工する

わざわざ一度ファイルに保存したり、複雑な変数を使ったりする必要はありません。

```PowerShell
# CSVを読み込んで、そのまま画面に綺麗に表示する（まだ通過させるだけ！）
Import-Csv ./member.csv | Out-Host
```

📄 6: 中間処理① 〜必要なデータだけ選ぶ（Select / Where）〜
データがパイプを流れてきたら、次はお好みに合わせて「加工（中間処理）」します。

1. 必要な「列（プロパティ）」だけを選ぶ：Select-Object（略称：sel）
「名前と役職だけが欲しい。年齢は不要！」という場合。

```PowerShell
# NameとRoleの列だけを抽出
Import-Csv ./member.csv | Select-Object Name, Role
```

```PowerShell
# 略称（エイリアス）を使って短く書く
Import-Csv ./member.csv | sel Name, Role
```

2. 条件に合う「行」だけを絞り込む：Where-Object（略称：where）
「Developer（開発者）だけを抽出したい！」という場合。

```PowerShell
# $_ は「今パイプラインを流れているそのデータ」を意味します
Import-Csv ./member.csv | Where-Object { $_.Role -eq "Developer" }
```

```PowerShell
# 略称を使って短く書く（-eq は Equal、つまり「＝」のこと）
Import-Csv ./member.csv | where Role -eq "Developer"
```

📄 7: 中間処理② 〜超強力なループ処理 ForEach-Object（%）〜
流れてきたデータ1件ずつに対して、「メールを送る」「フォルダを作る」「文字を加工する」といった独自の処理をしたいときは、ForEach-Object（略称：%）を使います。

全員の名前の後ろに「さん」を付けて挨拶する

```PowerShell
# % { } の中で、流れてきたデータを自由にいじれる
Import-Csv ./member.csv | ForEach-Object {
    Write-Host "こんにちは、$($_.Name) さん！"
}
```

```PowerShell
# 略称「%」を使って爆速で書く
Import-Csv ./member.csv | % { "名前: " + $_.Name }
```

💡 ポイント
$($_.Name) のように、$() で囲むと、文字列の中でオブジェクトの中身を安全に展開できます。

📄 8: 出力系① 〜画面で遊ぶ！神コマンド Out-GridView〜
加工したデータをファイルに保存する前に、画面で確認したいですよね。
そんな時に全PowerShellユーザーが愛してやまないのが Out-GridView（略称：ogv）です。

データを別ウィンドウのグリッド表示にする
```PowerShell
# CSVを読み込んでグリッドビューに投げる
Import-Csv ./member.csv | Out-GridView
```

```PowerShell
# 略称で書く
Import-Csv ./member.csv | ogv
```

これを実行すると、Excelのようなきれいな別ウィンドウが開きます。
なんと、その画面上で文字の検索や並び替え、フィルタリングがマウス操作で可能になります！デバッグや簡易ツールに最適です。

📄 9: 出力系② 〜成果物を保存する（CSV & Excel）〜
さあ、いよいよ最終段階です。加工したデータをファイルに出力して、上司や同僚に提出しましょう！

1. CSVに保存する（Export-Csv）
```PowerShell
# Developerだけを絞り込んで、新規CSVとして保存
Import-Csv ./member.csv | 
    where Role -eq "Developer" | 
    Export-Csv ./developers.csv -NoTypeInformation -Encoding UTF8
```

2. Excelに保存する（Export-Excel）
Page 4で入れた ImportExcel モジュールがあれば、出力も一瞬です。グラフやテーブル装飾も自動で付けられます！

```PowerShell
# データを読み込み、Excelとして出力（自動でテーブル装飾付き！）
Import-Csv ./member.csv | 
    Export-Excel ./output.xlsx -TableStyle Medium2 -AutoSize
```

これだけで、プロが作ったような綺麗なExcelファイルが完成します。

📄 10: 【総まとめ】これぞPowerShell！最強の1行レシピ
お疲れ様でした！最後に、これまで学んだ知識をすべて詰め込んだ「実戦向け1行コマンド（ワンライナー）」を作ってみましょう。

📌 ミッション
「CSVから読み込んだデータから、25歳以上の人だけを絞り込み、名前と役職のExcelファイルを作って、同時に画面でも確認する」

```PowerShell
Import-Csv ./member.csv | where Age -ge 25 | sel Name, Role | Out-GridView -PassThru | Export-Excel ./result.xlsx -AutoSize
```

🔍 一言解説

where Age -ge 25：25歳以上（Greater than or Equal）で絞り込み

sel Name, Role：必要な列だけ選んで

Out-GridView -PassThru：画面で確認し、OKなら「Enter」で次に流す！

Export-Excel ...：最終成果物のExcelが完成！

PowerShellは、まるでレゴブロックのようにコマンドを繋ぐだけで、強力なプログラムが作れます。ぜひ身の回りのファイルをたくさんいじって、楽しんでみてください！
