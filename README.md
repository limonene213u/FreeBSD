# FreeBSDで高可用性ファイルサーバー構築

## これはなに？
FreeBSDを用いた高可用性ファイルサーバーの構築に関しては、日本語情報が少なめです。  
ですから、自分の忘備録を兼ねてこちらにconfig等のファイルや検証結果を残しておき、共有しようという試みです。

## システム名称
**うなぎ㌠**  

## 開発プロセス概要
1. hyper-vを用いた検証環境で使用技術の練習と挙動確認
2. 本番環境を実機にデプロイ

## 使用する主なOS
1. FreeBSD 13.0
2. TrueNAS Scale
3. Truecommand
4. Ubuntu 22.04 LTS(Server)  
   ※Ubuntu上のdockerにTruecommandを入れて運用する予定

## 使用する技術
1. CARP(Common Adress Redundancy Protocol)  
   複数のサーバでIPアドレスを共有し、冗長化を実現するためのプロトコル  
2. HAST(Highly Available Storage)  
   2台のサーバ間でファイルシステムを同期して、高可用性ストレージを実現する技術  
3. Rgular file Filesystem  
   単一ファイルをファイルシステムとして使う技術  

# A.検証環境について

検証環境のうち、Hyper-Vを用いたFreeBSDの初期構成は以下の通りです。 

![Razer Blade 15 Hyper-V Network Ver 1 drawio (1)](https://user-images.githubusercontent.com/57677762/167357506-46127dc6-7cb3-4b5c-afcb-0bfd44c459fe.png)

## 説明
（作成中）
