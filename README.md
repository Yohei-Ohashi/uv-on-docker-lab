# Simple Docker + uv Python Environment

Mac・Windows（開発）+ Windows Server 2016（本番）のハイブリッド環境

## 使い方

### 開発環境（Mac・Windows）
```bash
# 対話的Python環境
docker compose run --rm python

# Pythonスクリプト実行
docker compose run --rm python uv run python your_script.py

# Jupyter起動
docker compose --profile jupyter up
# → http://localhost:8888/?token=simple-token-123
```

### Cursor + リモートウィンドウ開発
```bash
# 開発用コンテナを起動（バックグラウンド）
docker compose --profile dev up -d python-dev

# Cursorでコンテナにアタッチ
# Command Palette → "Dev Containers: Attach to Running Container" → python-dev

# 開発終了後、コンテナ停止
docker compose --profile dev down
```

### 本番環境（Windows Server 2016）
```powershell
# uvをインストール
Invoke-RestMethod https://astral.sh/uv/install.ps1 | Invoke-Expression

# 依存関係インストール・起動
uv sync
uv run jupyter lab --ip=0.0.0.0 --port=8888 --no-browser

# Pythonスクリプト実行
uv run python your_script.py
```

## 構成
- `pyproject.toml` - uv依存関係管理
- `Dockerfile` - Docker環境
- `docker-compose.yml` - 開発環境
- `README.md` - このファイル

以上！