# ActiveReportsJS Excel帳票インポート サンプル

ActiveReportsJSのExcelインポート機能を使用して、Excel帳票「売上報告書」をレポート定義へ変換し、JSON形式の売上データと連携してWebブラウザ上に表示するサンプルです。

毎月定期的に作成する社内向け資料を想定し、全社の売上概要、部門別実績、部門別売上明細を表示します。また、レポートパラメータを利用して、実行時に入力した備考を帳票へ反映します。

## サンプルの内容

このサンプルでは、主に次の内容を確認できます。

- Excel帳票のレイアウトを使用したWeb帳票
- JSON形式の売上データとの連携
- 全社の売上概要と部門別実績の集計
- 部門ごとの売上明細の表示
- レポートパラメータを使用した備考入力
- ActiveReportsJSの帳票ビューワによるレポート表示

## 関連記事

Excelファイル内へのTable領域の定義から、Excel帳票のインポート、JSONデータとの連携、レポートパラメータの設定、Webアプリケーションでの動作確認まで、以下の記事で詳しく解説しています。

- [ActiveReportsJSのExcelインポート機能を使って、Excel帳票をWeb化する！](https://devlog.mescius.jp/activereportsjs-excel-to-web-report/)


## ファイル構成

```text
.
├─ reports/
│  └─ sales-report.rdlx-json
├─ index.html
├─ package.json
├─ server.js
└─ 売上報告書レイアウト.xlsx
```

| ファイル／フォルダ | 内容 |
|---|---|
| `reports/` | ActiveReportsJSのレポート定義ファイルを格納するフォルダ |
| `sales-report.rdlx-json` | Excel帳票を基に作成したレポート定義ファイル |
| `index.html` | ActiveReportsJSの帳票ビューワを表示するWebページ |
| `package.json` | サンプルで使用するパッケージ情報 |
| `server.js` | Webアプリケーションを起動するためのサーバースクリプト |
| `売上報告書レイアウト.xlsx` | Excelインポートに使用する売上報告書のレイアウトファイル |

## 動作環境

- Node.js
- npm
- ActiveReportsJS
- Webブラウザ

Node.jsはLTSバージョンの利用を推奨します。

## サンプルの実行方法

### 1. リポジトリを取得する

```powershell
git clone https://github.com/MESCIUSJP/import-excel-arjs-js-viewer-app.git
cd import-excel-arjs-js-viewer-app
```

### 2. パッケージをインストールする

```powershell
npm install
```

### 3. Webアプリケーションを起動する

```powershell
node .\server.js
```

起動後、WebブラウザでWebアプリケーションを開きます。

### 4. レポートをプレビューする

パラメータパネルの［備考入力］に任意の内容を入力し、プレビューボタンをクリックします。

レポートが表示されたら、次の内容を確認します。

- 1ページ目に、全社の売上概要と部門別実績が表示される
- 入力した内容が、売上報告書の備考欄に反映される
- 2ページ目以降に、各部門の売上明細が表示される
- 売上高、達成率、前年比、粗利益、粗利率が集計される

## Excel帳票について

`売上報告書レイアウト.xlsx` には、ActiveReportsJSへTableデータ領域として取り込むための名前を定義しています。

### 売上報告書シート

| 対象 | 定義名 |
|---|---|
| 表全体 | `ARTable1` |
| 見出し行 | `ARTable1.TableHeader` |
| 明細領域 | `ARTable1.Detail` |
| 合計行 | `ARTable1.TableFooter` |

### 営業第一部シート

| 対象 | 定義名 |
|---|---|
| 表全体 | `ARTable2` |
| 見出し行 | `ARTable2.TableHeader` |
| 明細領域 | `ARTable2.Detail` |
| 合計行 | `ARTable2.TableFooter` |

Excelファイル内の表に名前を定義することで、Excelインポート時に表形式の領域をTableデータ領域として取り込めます。

## レポートの構成

作成したレポートは、次のページで構成されています。

### 売上報告書ページ

- 対象年月
- 全社の売上概要
- 部門別実績
- 備考
- 評価基準

### 部門別売上明細ページ

- 部門名と対象年月
- 部門単位の売上実績
- 売上明細
- 売上金額、粗利益、粗利率の合計

## データセット

レポートでは、次の2つのデータセットを使用します。

### `Departments`

全社および各部門の基本情報、目標金額、前年実績を保持します。

主なフィールド：

- `deptCode`
- `deptSort`
- `deptName`
- `yearMonth`
- `targetAmount`
- `previousYearAmount`

### `SalesDetails`

各部門の売上明細を保持します。

主なフィールド：

- `deptCode`
- `date`
- `customer`
- `project`
- `amount`
- `grossProfit`
- `grossMargin`
- `owner`

`deptCode` を使用して、部門情報と売上明細を関連付けます。

## レポートパラメータ

備考入力用として、文字列型の `Notes` パラメータを使用します。

| プロパティ | 設定値 |
|---|---|
| 名前 | `Notes` |
| ダイアログの表示文字列 | `備考` |
| データタイプ | `String` |
| 複数行表示 | はい |
| 空白の値を許可する | はい |

入力した値は、売上報告書ページの備考TextBoxに表示されます。

## 製品情報

- [ActiveReportsJS 製品ページ](https://developer.mescius.jp/activereportsjs)
- [ActiveReportsJS Excelインポート](https://demo.mescius.jp/activereportsjs/docs/v6/ReportAuthorGuide/Import)

## 注意事項

- このサンプルは、ActiveReportsJSの機能を紹介する目的で作成しています。
- Excel帳票、売上データ、会社名、部門名、顧客名などはサンプル用の内容です。
- 実際の業務で使用する場合は、データソース、レポート定義、表示内容を利用環境に合わせて変更してください。
