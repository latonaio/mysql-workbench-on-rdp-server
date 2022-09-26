# mysql-workbench-on-rdp-server
mysql-workbench-on-rdp-server はRDP サーバー上にMySQL Workbenchをインストールする手順概要です。

# AWS 上の RDP サーバー構築

RDP サーバー用のEC2 インスタンスを作成します。

- [EC2 インスタンス](https://us-west-2.console.aws.amazon.com/ec2/home?region=us-west-2#Home:)から「インスタンスを起動」を選択します。

- 以下の項目を設定します。
  
  - 名前：インスタンス名を入力します。
  - アプリケーションおよび OS イメージ (Amazon マシンイメージ)：「Microsoft Windows Server 2022 Base」で検索し、画面遷移後、「選択」をクリックします。
  - インスタンスタイプ：「t2.medium」を選択します。
  - キーペア（ログイン）：既存のキーペアを選択もしくは新しいキーペアを作成します。
  - VPC：MySQL を含むVM と同じVPC を選択します。
  - サブネット：対象のMySQL のVPC のパブリックのサブネットを割り当てる。
  - ファイアウォール（セキュリティグループ）：port 3389 が空いているセキュリティグループを作成します。

- 以上の設定項目を入力したのち、「インスタンスを起動」を選択します。

# RDP サーバーへの接続

## AWS における初期設定
RDP サーバーへの接続方法のAWS における初期設定を行います。

- 作成したEC2 インスタンスの「インスタンスID」を選択します。

- 右上の「接続」を選択します。

- 「RDP クライアント」タブを選択し、「リモートデスクトップファイルのダウンロード」をクリックします。
  - RDP ファイルがダウンロードされます。

- 「パスワードを取得」をクリックし、画面遷移後、インスタンスのキーペアを参照し、「パスワードを復号化」を選択します。

- パスワードが表示されるので、コピーし、記録しておきます。

## リモートデスクトップツールにおける初期設定
RDP サーバーへの接続方法のリモートデスクトップツールにおける初期設定を行います。

- ダウンロードしたRDP ファイルとコピーしたパスワードを利用し、各ツールの手順に従って、RDP サーバーに接続します。

### Mac での手順例

#### リモートデスクトップツールのインストール
Microsoft Remote Desktop をローカルPC にダウンロードします。

- [Microsoft Remote Desktop](https://apps.apple.com/jp/app/microsoft-remote-desktop/id1295203466?mt=12)

#### Microsoft Remote Desktop における初期設定
RDP サーバーへの接続方法のMicrosoft Remote Desktop における初期設定を行います。

- Microsoft Remote Desktop を起動します。

- ダウンロードしたRDP ファイルをドラッグ&ドロップします。

- 登録されたリモートデスクトップをダブルクリックし、コピーしたパスワードを入力し、立ち上げます。


# Workbench のインストール
リモートデスクトップにWorkbench をインストールします。

- [MySQL Installer](https://dev.mysql.com/downloads/installer/)からmysql-installer-web-community-8.0.30.0.msi の「Download」を選択します。

- 「No thanks, just start my download.」をクリックします。

- ダウンロードした「mysql-installer-web-community-8.0.30.0.msi」を実行し、指示に従ってSetup を進めます。

- Setup が完了したら、「MySQL Workbench 8.0CE」をクリックし、Workbench を起動します。



# Workbench の基本操作

## リモートサーバーのMySQL への接続
- 「MySQL Connections」横の+マークをクリックします。

- 以下の情報を入力し、OK をクリックします。

	- Connection Name：connection の名前を入力します。
	- Hostname：リモートサーバーのIP アドレスを入力します。
	- Port：リモートサーバーのport 番号を入力します。
	- Username：リモートサーバーのuser name を入力します。
	- Password：Username におけるpassword を入力します。
	- Default Schema：リモートサーバーのデータベース名を入力します。

## データベースの確認
- 左の「Navigator」タブの下側にある「Schemas」をクリックすると、データベースの一覧が表示されます。

## テーブルの確認
- 左の「Schemas」欄からデータベースを選択します。

- 「Tables」をクリックすると、テーブルの一覧が表示されます。

- 選択したいテーブルを右クリックします。

- 「Select Rows - Limit 1000」をクリックすると、テーブルの中身が表示されます。

## データベースの作成
- 上の絵文字が並んだタブの左から4 番目をクリックします。

- 「Name」にデータベース名を入力し、「Apply」をクリックします。

- 再び「Apply」をクリックすると、データベースが作成されます。

## テーブルの作成
- 上の絵文字が並んだタブの左から5 番目をクリックします。

- 「Table Name」にテーブル名を入力します。

- 右の二重上矢印を押し、カラムの登録画面に遷移します。

- 「Column Name」、「Datatype」等を入力し、「Apply」をクリックします。

- 再び「Apply」をクリックすると、テーブルが作成されます。