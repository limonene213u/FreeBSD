# FreeBSDで高可用性ファイルサーバー構築の概要

## これはなに？
FreeBSDを用いた高可用性ファイルサーバーの構築に関しては、日本語情報が少なめです。  
ですから、自分の忘備録を兼ねてこちらにconfig等のファイルや検証結果を残しておき、共有しようという試みです。

## システム名称と命名規則
名付けて**うなぎ㌠** です！  
   * 各ノードの命名はUNA-[数字]とします。

## 検証環境を構築する意義
1. hyper-vを用いた検証環境で使用技術の向上と挙動確認
2. 実装された最新機能の随時テスト  
  従って、この検証環境は恒久的に使えるようにしておきます。

## 使用する主なOS
1. FreeBSD 13.0
2. TrueNAS Scale
3. Truecommand
4. Ubuntu 22.04 LTS(Server)  
   ※Ubuntu上のdockerにTruecommandを入れて運用する予定

## ファイルサーバーで使用する主な技術
1. CARP(Common Adress Redundancy Protocol)  
   複数のサーバでIPアドレスを共有し、冗長化を実現するためのプロトコル  
2. HAST(Highly Available Storage)  
   2台のサーバ間でファイルシステムを同期して、高可用性ストレージを実現する技術  
3. Rgular file Filesystem  
   単一ファイルをファイルシステムとして使う技術  

# A.検証環境について
* [検証環境について](https://github.com/limonene213u/FreeBSD/blob/main/test_env/readme.md)
<br>
# 本番環境について（予定）
「いま現在、別の本番環境で使用している機材のほうが使用感が分かって良い」という認識のもと、これらの機材を使うことを想定しています。
## 使用機材
* HPE DL360e Gen8  
  Xeon E5-2670 V2×2（20C40T）  
  RAM:80GB  
  Strage：2TB（Full SSD、RAID6）
  >FreeBSD用に2台使用します
* HPE ML310e Gen8 V2    
  Xeon E3-1280 V3（4C8T）  
  RAM：32GB  
  Strage：4TB（SAS HDD、RAID-Z）
  >TrueNAS Scale用に3台使用します
* AlliedTelesis AT-X510-28GTX
  >コアスイッチ
