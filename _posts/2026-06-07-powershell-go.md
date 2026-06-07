---
layout: post
title: powershell-パイプでGo！
date: 2026-06-07 10:00:00 +0900
last_modified_at: 2026-06-07 10:00:00 +0900
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
  1. で、この後ろにパイプ記号を追加します。キーボード右上のほうの¥記号のキーをshiftキーを押しながら押すと | 縦棒の記号が現れる！これがパイプです。この記事ではこのパイプの利用のメリットや使い方にフォーカスして話を進めます。
  1. で、今打ち込んだパイプ記号の後ろに ogvと半角で打ち込んでenterを押してみて！  
  <img src="/assets/img/pipe1st.png" alt="pp1" width="200">  
  1. こんなの出た？  
  <img src="/assets/img/ogv1st.png" alt="og1" width="360">  
  



