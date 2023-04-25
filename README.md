# sommelier_app

## ディレクトリ構成
```
sommelier-app/
  ├─ android/                       Androidアプリのフォルダ
  │     (基本修正禁止)
  ├─ assets/                        画像・フォントファイルなど
  ├─ docs/                        ドキュメント・Github Pagesのファイルなど
  ├─ ios/　　　　　　　　　　　　　　　　iOSアプリのフォルダ
  │     (基本修正禁止)
  ├─ lib/　　　　　　　　　　　　　　　(Flutterソースコード本体)
  │    ├ Entity/(ビジネスロジックを表現するデータ/model)
  │    ├ query/(データを取得するビジネスロジック)
  │    ├ Gateways/ (データベースとの通信箇所)
  │    ├ presenter/ (状態を保持して、Viewに渡す)
  │    ├ ui/ (View、画面単位で分割)
  │    │ └ presenter/ (各画面単位での状態管理)
  │    ├ util/ (インスタンス化する意味がないもの群 例)アップデートが必要な時にだすポップ等)
  │    ├ widgets/ (共通部品Widget　例)自分たちで作ったボタン等）
  │    └theme/ (色や文字フォント、サイズを管理)
  │
  ├─ test/　　（自動テストコードフォルダ）
  ├─ .gitignore  (git管理除外設定用ファイル)
  ├─ analysis_options.yaml  (静的解析ツール)
  └─ pubspec.yaml  (パッケージライブラリ)
```

## 画面遷移方法
下記方法を採用

Navigator.push(
context,
MaterialPageRoute(builder: (context) => クラス名()),
);

## プロジェクトツール一覧

| タイトル | 内容 |
| --- | --- |
| jooto | https://app.jooto.com/boards#912561?organization_id=275999 |
|  ドキュメント |  |
| bitrise |  |
| firebase |  |

### プライバシーポリシーページ
url : 

## ブランチ運用
### 固定ブランチ
- main: リリース用ブランチ（prod版stable）
- develop: 開発用ブランチ（beta版アプリ）

### 開発の流れ

- 各featureの開発
- リリースビルド ※このプロジェクトではなし

### 各featureの開発

基本的にWBSチケット単位で機能開発
チケットがない場合はつくり、あるけど他の機能も含まれてしまう場合は子タスク登録するか分割しましょう。

1.最新のdevからbranchを切る  
何をするブランチなのかわかる名前のほうが良い（例：新機能→feature/hoge、バグ修正→fix/fuga）。

2.機能開発後、devに向けてプルリクエスト  
詳細のところにWBSチケットのリンクを貼ったり、簡単な説明書を入れると数ヶ月後でも何をしたかが追えるので推奨。

3.レビューを依頼し、approveされたらdevにマージ(レビューは中洲様に向けてください)
↓  
devブランチへマージされると、betaのflavorで自動的にbitriseでビルドされる。  
iOSはtestflightへ配布され、androidはslackの通知の"Install Page"からインストールできる。

4.動作確認  