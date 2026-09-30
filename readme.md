# CatTax - 猫行動分析システム（YOLO11）

コンピュータビジョンに基づく猫の行動分析システムで、動画内の猫の行動状態をリアルタイムで検出・分析できます。

## 主な機能

- 猫のリアルタイム検出と追跡
- 行動状態の分析（歩行、休息、立ち上がりなど）
- 複数の猫の同時分析
- リアルタイムな可視化結果

## システム要件

- Python 3.8+
- Node.js 14+
- Redis サーバー
- CUDA（オプション、GPU 高速化に使用）

## インストール手順

1. リポジトリをクローン
  
  ```bash
  git clone https://github.com/ibaratorii/cattax.git
  cd cattax
  ```
  
2. Python 仮想環境を作成して有効化
  
  Windows
  
  ```bash
   python -m venv venv
   venv\Scripts\activate
  ```
  
  Linux/Mac
  
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
  
3. 依存関係をインストール
  
  ```bash
  pip install -r requirements.txt
  ```
  
4. フロントエンドの依存関係をインストール
  
  ```bash
  cd frontend
  npm install
  ```
  
5. 環境変数を設定
  
  ```bash
  環境変数のサンプルファイルをコピー
  cp .env.example .env
  
  必要に応じて .env ファイルを編集
  ```
  
6. データベースを初期化
  
  ```bash
  python manage.py makemigrations
  python manage.py migrate
  ```
  
7. YOLO モデルファイルを配置
  
  YOLO モデルファイル `yolo11x-seg.pt` は別途ダウンロードする必要があります：
  
  1. ダウンロード先：[リンク]
  2. ファイルをプロジェクトのルートディレクトリに配置

## サービスの起動

4 つのターミナルを起動する必要があります：

> **注意**: Celery を起動する前に、必ず Redis サーバー（ターミナル 1）を起動してください。

### ターミナル 1: Redis サーバー

```bash
redis-server
```

### ターミナル 2: Celery worker

```bash
仮想環境を有効化した後
celery -A cattax worker -l info
```

### ターミナル 3: Django サーバー

```bash
python manage.py runserver
```

### ターミナル 4: フロントエンド開発サーバー

```bash
cd frontend
npm run serve
```

## 使用方法

1. http://localhost:8080 にアクセス
2. 猫の動画ファイルをアップロード
3. システムの分析を待つ（分析時間は動画の長さによって異なります）
4. 分析結果を確認

## プロジェクト構成

```text
cattax/
├── api/                # Django API アプリケーション
├── cattax/             # メインプロジェクトディレクトリ
│   ├── cat_capture.py  # 猫検出モジュール
│   └── cat_behavior.py # 行動分析モジュール
├── frontend/           # Vue.js フロントエンドアプリケーション
├── manage.py           # Django 管理スクリプト
├── requirements.txt    # 依存パッケージリスト
└── .env.example        # 環境変数サンプルファイル
```

## ライセンス

MIT License
