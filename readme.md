azure-cli-modules
===

# Description
Azure CLIを利用した自動構築スクリプト集

* azureDatabase  
Azure Database for MySQL自動構築スクリプト。将来Postgre, MariaDB向けスクリプトを実装予定。
  * 文字コードはutf-8
  * TimezoneはAzire/Tokyo

* loadBalancer  
Application Gateway自動構築スクリプト。将来Load Balancer向けスクリプトを実装予定。  
  * SSLオフロード
  * マルチサイト
  * httpsリダイレクト
  
* staticWebHostingInAzureStorage  
静的サイトホスティング向けAzure Storage構築スクリプト。将来CDNとの連携スクリプトを実装予定。

* virtualMachine  
VM内のパッケージインストール、ディレクトリインストール込みの構築スクリプト。
  * CentOS7ベース
  * SELinux無効
  * 文字コードUTF-8, TimezoneはAzire/Tokyo
  * NTP同期先変更
  * Apache, PHP, MySQL Clientインストール
  * Virtualhostで本番、テストの2環境設定
  * 独自ドメイン、SSLインストール、バックアップ、データディスクアタッチ設定は手動で実装のこと

* webApps  
Windows版Webapp構築スクリプト。
  * App Service Plan1インスタンス内にネイキッド用、www用、テスト用のWebappsをプロビジョニング
  * ディレクトリ構成はLaravelを想定
  * テストにはDigest認証を実装
  * TimezoneはAzire/Tokyo
  * DB接続情報はアプリケーション設定（環境変数）にて定義
  * 独自ドメイン、SSLインストール、バックアップ設定は手動で実装のこと

* webAppsOnLinux  
Bulit-inイメージ自動。将来Webapps for Containerとして魔改造Dockerイメージをベースとした自動構築を実装予定。  
※現在検証中のため、調整が必要です。
  * App Service Plan1インスタンス内にネイキッド用、www用、テスト用のWebappsをプロビジョニング
  * ディレクトリ構成はLaravelを想定
  * テストにはBasic認証を実装
  * TimezoneはAzire/Tokyo
  * 独自ドメイン、SSLインストール、バックアップ設定は手動で実装のこと

# Requirement  
* [Azure CLI](https://docs.microsoft.com/ja-jp/cli/azure/install-azure-cli?view=azure-cli-latest)
* Bash

# Usage

```
# ローカルDL
$git clone https://github.com/pir0000w/azure-cli-modules.git

# 変数ファイル編集
$cp conf.txt.example conf.txt
$vi conf.txt

#　（VMを利用する場合のみ）スタートアップスクリプトの変数編集
$cd virtualMachine
$vi Centos7startup.sh

# Azure ログイン
$az login

# サブスクリプション設定
$az account show
$az account list -o table
$az account set -s <Subscription ID>

# リソースグループ作成
$bash common.azcli

# リソース作成
$cd <Directory name>
$bash xxx.azcli

# リソース削除
$bash clean.azcli
```