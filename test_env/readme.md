# A.検証環境について（Ver.1.0）

検証環境のうち、Hyper-Vを用いたFreeBSDの初期構成は以下の通りです。<br>
ちょうど手持ちですので[Razer Blade 15(Basemodel)](https://mysupport.razer.com/app/answers/detail/a_id/2573/~/at-a-glance%3A-razer-blade-15-base-%282018%29-%7C-rz09-02705)のWindows上に構築します。  

![Razer Blade 15 Hyper-V Network Ver 1 drawio (1)](https://user-images.githubusercontent.com/57677762/167357506-46127dc6-7cb3-4b5c-afcb-0bfd44c459fe.png)

## Razer Blade15上に構築する理由  
   スペックが高く、可搬性が高いからです。  
   使用するBlade15ですが、プロセッサ（Intel Core(TM) i7-8750H）は6C12Tもあり、RAMも32GB積んでいます。ですから、多数のVMを立ち上げることに適した構成であると判断しました。  
   本当は64GBほどRAMが積める方が良い（ZFSを使うため、TrueNASは１ノードあたり最低8GB必要）のですが、そのようなモバイルワークステーションが手許にないのでこのような構成にしました。  
   移動中でも、出先でも、ネットワークがない場所でも作業自体は進められるような環境を構築したかったということもあります。    
   （とはいえ、今後システムの規模が大きくなってどうしても手狭になったら検証用に1Uサーバーを使うような気はする）  
<br/>
## ネットワーク構成について（External編）<br>
   パッケージ更新やソフトウェアのインストール等、外部との通信にあたってはHyper-v内に仮想スイッチを２つ作成し、それぞれWifiと有線のポートを用いて通信が行えるようにしました。<br>
   BSD上からはhn0（無線側）、hn1（有線側）の２つのNICを用いて外部と通信ができるようになっています。<br>
   どちらの回線を使うかは、Windows上の各ポートのメトリックで自動的に決定します。また、外向けの通信の目的ですが、pkgを使えれば事足りますので、ipはfixにはしていません。<br>
    むしろどのネットワークに接続しても通信が行えるよう、DHCPで接続情報を随時取得できるようにしています(これが"wanna be able to use on-the-spot network(s)"を実現したところ)。<br>
    <br>
   > 余談：SSHに関しては、Tera Termを用いて次に記述する内部スイッチ向きに疎通を図っても、通常通り行うことができました。
## ネットワーク構成について（Internal編）<br> 
  （以下編集中）
