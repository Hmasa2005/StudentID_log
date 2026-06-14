# StudentID_log

<img src="/sample/IMG_0311.jpeg" alt="StudentID_log" width="300">

学生証の入退室ログを Google スプレッドシートに記録するアプリケーションです。

## 対応カードリーダー

- Sony PaSoRi **RC-S380 シリーズのみ対応**

## 重要: PaSoRi認識の事前作業

このアプリが RC-S380 を認識するには、先に以下の作業が必要です。

- 参考手順: https://obenkyolab.com/?p=741

未実施の場合、カードリーダー関連エラーになります。

## 動作環境

- Windows
- `.exe`

## 配布ファイル構成（利用者向け）

`.exe` 配布時は、以下を **同じフォルダ** に配置してください。

- `StudentID_log.exe`
- `GoogleAPI.json`
- `SheetID.txt`
- `strings.json`
- `img/`
- `AD_images/`

例:

```text
StudentID_log/
  StudentID_log.exe
  GoogleAPI.json
  SheetID.txt
  strings.json
  img/
  AD_images/
```

## 初期設定（.exe利用者向け）

### 1. PaSoRi を準備

- RC-S380 シリーズを接続
- 上記リンクの手順を実施

### 2. Google API 認証ファイルを配置

- GoogleAPI は、Google API からスプレッドシート編集ボットを登録したときに発行された json ファイルを配置し、`strings.json` の `google_api_path` にパスを指定してください。

`strings.json` 例:

```json
{
  "google_api_path": "GoogleAPI.json"
}
```

## Google API 初期設定（詳細）

以下は、Google スプレッドシートを API で操作するための準備手順です。

- Google Cloud Console: https://console.cloud.google.com/

### 1. API接続用の認証情報（JSON）を取得

1. GCP でプロジェクトを作成する。
2. 左メニューから「API とサービス」>「認証情報」を開く。
3. 画面上部の「+ 認証情報を作成」>「サービス アカウント」を選択する。
4. 必要項目を入力してサービスアカウントを作成する。
5. 作成したサービスアカウントを開き、「キー」タブを選択する。
6. 「鍵を追加」>「新しい鍵を作成」を選択する。
7. 「JSON」形式を選択して作成する。
8. ダウンロードされた JSON ファイルを安全な場所に保管する。

### 2. 必要な API を有効化

1. 「API とサービス」>「有効な API とサービス」を開く。
2. 「+ API とサービスの有効化」を選択する。
3. API ライブラリで以下 2 つを検索して有効化する。

- Google Drive API
- Google Sheets API

### 3. 対象 Spreadsheet に API アクセス権を付与

1. 取得した JSON ファイルを開き、`client_email` の値をコピーする。
2. アクセス対象の Google スプレッドシートを開く。
3. 右上の「共有」を押す。
4. 「ユーザーやグループを追加」に `client_email` のメールアドレスを貼り付ける。
5. 権限を「編集者」にして送信する。

上記で API 利用の準備は完了です。

### 3. スプレッドシートIDを設定

`SheetID.txt` を以下の形式で設定:

```txt
SheetID=あなたのスプレッドシートID
```

### 4. スプレッドシート共有設定

- `GoogleAPI.json` のサービスアカウントメールを共有先に追加
- 権限は「編集者」を推奨

## 起動方法（.exe）

- `StudentID_log.exe` をダブルクリック

## よくあるエラー

### Spreadsheet error: APIError: [403]: The caller does not have permission

原因:

- サービスアカウントに共有権限がない
- 誤った `GoogleAPI.json` を読んでいる

確認ポイント:

- `SheetID.txt` が正しいか
- `strings.json` の `google_api_path` が正しいか
- スプレッドシート共有にサービスアカウントが追加済みか

### カードリーダーを認識しない

- RC-S380 シリーズか確認
- 事前作業（https://obenkyolab.com/?p=741）が完了しているか確認

## 配布者向けチェックリスト

- `GoogleAPI.json` は公開リポジトリにコミットしない
- `SheetID.txt` はテンプレート値で配布する
- `strings.json` の `google_api_path` が配布構成に合っているか確認
- `img/` と `AD_images/` が同梱されているか確認
- 実機で RC-S380 読み取りテストを実施


