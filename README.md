# PDF Q&A アプリケーション

このプロジェクトは、フォルダ内に保存されているPDFファイルの内容をもとに質問に答えるQ&Aアプリケーションです。
以下の技術を使用して構築されています：

- Django
- HTMX
- LangGraph
- PostgreSQL
- Docker

## 主な機能

1. **PDFのアップロードと内容の保存**
   - フォルダ内にあるPDFファイルを読み取り、データベースに内容を保存します。

2. **自然言語での質問応答**
   - 保存されたPDFの内容に基づいて、質問に対する回答を生成します。

3. **リアルタイム応答**
   - HTMXを使用して、質問への応答を非同期で更新します。

---

## 環境構築

### 必要なツール
- Docker / Docker Compose
- Python 3.11以上
- pip

### セットアップ手順

1. **リポジトリのクローン**
   ```bash
   git clone <リポジトリURL>
   cd pdf_qa_app
   ```

2. **依存関係のインストール**
   プロジェクトのルートディレクトリにある`requirements.txt`を使用して、Python依存関係をインストールします：
   ```bash
   pip install -r requirements.txt
   ```

3. **Dockerの設定**
   Dockerを使用してアプリケーションをコンテナ化します。

   **Dockerコンテナをビルドして起動**:
   ```bash
   docker-compose up --build
   ```

4. **データベースのマイグレーション**
   初期設定として、データベーススキーマを作成します。
   ```bash
   docker-compose exec web python manage.py makemigrations
   docker-compose exec web python manage.py migrate
   ```

5. **PDFデータの読み込み**
   PDFファイルを指定フォルダから読み込んでデータベースに保存します。
   ```bash
   docker-compose exec web python manage.py shell
   ```
   シェル内で以下を実行してください：
   ```python
   from qanda.utils import load_pdfs_from_folder
   load_pdfs_from_folder('/path/to/pdf/folder')
   ```

---

## 使用方法

1. **アプリケーションの起動**
   ブラウザで以下のURLにアクセスします：
   ```
   http://localhost:8000
   ```

2. **質問を入力**
   ホームページのフォームに質問を入力し、「質問する」ボタンを押します。

3. **回答の確認**
   PDFデータに基づく回答がリアルタイムで表示されます。

---

## プロジェクト構成

```
pdf_qa_app/
├── Dockerfile
├── docker-compose.yml
├── manage.py
├── pdf_qa_app/
│   ├── settings.py
│   ├── urls.py
│   └── ...
├── qanda/
│   ├── models.py
│   ├── views.py
│   ├── utils.py
│   ├── langchain_utils.py
│   └── templates/qanda/index.html
├── requirements.txt
└── ...
```

---

## 今後の改善点

- PDFのアップロード機能をWebインターフェースに追加
- ユーザーごとにPDFを管理できる認証システムの導入
- 回答精度の向上のためのAIモデルのカスタマイズ

---

## ライセンス

このプロジェクトはMITライセンスのもとで公開されています。

