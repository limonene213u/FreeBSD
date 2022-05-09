# FreeBSDで高可用性ファイルサーバー構築（ほぼ趣味）

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

# A.検証環境について（Ver.1.0）

検証環境のうち、Hyper-Vを用いたFreeBSDの初期構成は以下の通りです。<br>
Razer Blade 15(Basemodel)のWindows上に構築します。  

![Razer Blade 15 Hyper-V Network Ver 1 drawio (1)](https://user-images.githubusercontent.com/57677762/167357506-46127dc6-7cb3-4b5c-afcb-0bfd44c459fe.png)

## Razer Blade15上に構築する理由  
   スペックが高く、可搬性が高いからです。  
   使用するBlade15ですが、プロセッサ（Intel Core(TM) i7-8750H）は6C12Tもあり、RAMも32GB積んでいます。ですから、多数のVMを立ち上げることに適した構成であると判断しました。  
   本当は64GBほどRAMが積める方が良い（ZFSを使うため、TrueNASは１ノードあたり最低8GB必要）のですが、そのようなモバイルワークステーションが手許にないのでこのような構成にしました。  
   移動中でも、出先でも、ネットワークがない場所でも作業自体は進められるような環境を構築したかったということもあります。    
   （とはいえ、今後システムの規模が大きくなってどうしても手狭になったら1Uサーバーを使うような気はする）  
<br/>
## ネットワーク構成について（External編）<br>
   パッケージ更新やソフトウェアのインストール等、外部との通信にあたってはHyper-v内に仮想スイッチを２つ作成し、それぞれWifiと有線のポートを用いて通信が行えるようにしました。<br>
   BSD上からはhn0（無線側）、hn1（有線側）の２つのNICを用いて外部と通信ができるようになっています。<br>
   どちらの回線を使うかは、Windows上の各ポートのメトリックで自動的に決定します。また、外向けの通信はpkgを使えれば事足りますので、fixにはしていません。<br>
    むしろどのネットワークに接続しても通信が行えるよう、DHCPで接続情報を随時取得できるようにしています。<br>
    <br>
   > 余談：SSHに関しては、Tera Termを用いて次に記述する内部スイッチ向きに疎通を図っても、通常通り行うことができました。
## ネットワーク構成について（Internal編）<br> 
  （以下編集中）
<br>
# 本番環境について（予定）
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
  >TrueNAS Scale用に台使用します
* AlliedTelesis AT-X510-28GTX