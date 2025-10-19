# stock-project-20251019-start-test
Test codex and try start a auto record and analyze model for the stock information.
MIT License

# 📈 Stock Analysis Platform

一個整合台股與美股資料的股票分析平台，提供即時資料、技術指標分析與機器學習預測功能。

## ⚠️ 重要免責聲明

**本軟體僅供教育和研究用途，不構成任何投資建議。**

- 本平台提供的所有資訊、分析和預測結果僅供參考
- 投資有風險，past performance 不代表未來表現
- 使用者應自行判斷並為投資決策負責
- 開發者不對任何投資損失承擔責任
- 請在投資前諮詢專業財務顧問

## ✨ 功能特色

- 📊 **多市場資料整合**：台股(TWSE/TPEX) 與美股資料
- 🔄 **即時資料更新**：自動化資料抓取與更新機制
- 📈 **技術指標分析**：MA, RSI, MACD, 布林通道等
- 🤖 **機器學習預測**：基於歷史資料的趨勢預測（實驗性功能）
- 🎨 **互動式圖表**：直觀的資料視覺化介面
- ⚡ **高效能 API**：FastAPI 後端，快速回應

## 🏗️ 專案架構

```
stock-project/
├─ README.md
├─ docs/                      # 詳細文件
│  ├─ API.md                  # API 使用說明
│  ├─ DEPLOYMENT.md           # 部署指南
│  └─ DATA_SCHEMA.md          # 資料欄位說明
├─ backend/                   # FastAPI 後端服務
│  ├─ app/
│  │  ├─ main.py
│  │  ├─ api/                 # API endpoints
│  │  ├─ services/            # 業務邏輯
│  │  ├─ models/              # 資料庫模型
│  │  └─ config.py
│  ├─ Dockerfile
│  └─ requirements.txt
├─ data_fetcher/              # 資料抓取與 ETL
│  ├─ fetch_twse.py           # 台股資料
│  ├─ fetch_us.py             # 美股資料
│  └─ scheduler.py            # 排程器
├─ ml/                        # 機器學習模組
│  ├─ features/               # 特徵工程
│  ├─ models/                 # 模型定義
│  ├─ train.py                # 訓練腳本
│  └─ predict_api.py          # 預測服務
├─ frontend/                  # React 前端
│  ├─ package.json
│  ├─ src/
│  └─ Dockerfile
├─ infra/                     # 基礎設施配置
│  ├─ docker-compose.yml
│  └─ k8s/                    # Kubernetes (選用)
├─ .github/workflows/
│  └─ ci.yml                  # CI/CD 流程
└─ tests/
   ├─ backend/
   └─ ml/
```

## 🚀 快速開始

### 前置需求

- Docker & Docker Compose
- Python 3.11+
- Node.js 18+

### 使用 Docker Compose 啟動

```bash
# 克隆專案
git clone https://github.com/your-username/stock-project.git
cd stock-project

# 複製環境變數範本
cp .env.example .env

# 編輯 .env 填入必要的 API keys
# TWSE_API_KEY=your_key
# ALPHA_VANTAGE_API_KEY=your_key

# 啟動所有服務
docker-compose up -d

# 查看日誌
docker-compose logs -f
```

服務啟動後：
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- API Docs: http://localhost:8000/docs

### 本地開發

#### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

#### Frontend

```bash
cd frontend
npm install
npm run dev
```

#### 資料抓取

```bash
cd data_fetcher
python fetch_twse.py  # 抓取台股資料
python fetch_us.py    # 抓取美股資料
```

## 📖 文件

詳細文件請參閱 `docs/` 目錄：

- [API 文件](docs/API.md) - 完整的 API 端點說明
- [部署指南](docs/DEPLOYMENT.md) - 生產環境部署步驟
- [資料欄位](docs/DATA_SCHEMA.md) - 資料庫 schema 與欄位說明

## 🧪 測試

```bash
# 執行所有測試
pytest

# 執行特定模組測試
pytest tests/backend/
pytest tests/ml/

# 生成測試覆蓋率報告
pytest --cov=app --cov-report=html
```

## 🛠️ 技術棧

### Backend
- **FastAPI** - 現代化的 Python Web 框架
- **SQLAlchemy** - ORM
- **PostgreSQL** - 主要資料庫
- **Redis** - 快取層
- **Pandas** - 資料處理

### ML
- **scikit-learn** - 傳統機器學習
- **TensorFlow/PyTorch** - 深度學習（選用）
- **TA-Lib** - 技術指標計算

### Frontend
- **React** - UI 框架
- **Chart.js / Recharts** - 圖表視覺化
- **TailwindCSS** - 樣式

### DevOps
- **Docker** - 容器化
- **GitHub Actions** - CI/CD
- **Kubernetes** - 容器編排（選用）

## 🔑 環境變數配置

創建 `.env` 檔案：

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/stockdb

# Redis
REDIS_URL=redis://localhost:6379

# API Keys
TWSE_API_KEY=your_twse_key
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key

# ML Models
MODEL_PATH=/app/ml/models/

# App Settings
DEBUG=False
SECRET_KEY=your-secret-key
```

## 🤝 貢獻指南

歡迎貢獻！請遵循以下步驟：

1. Fork 本專案
2. 創建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交變更 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 開啟 Pull Request

### 程式碼規範

- Python: 遵循 PEP 8，使用 `black` 格式化
- JavaScript: 使用 ESLint + Prettier
- Commit messages: 使用 [Conventional Commits](https://www.conventionalcommits.org/)

## 📊 資料來源聲明

本專案使用以下資料來源：

- **台灣證券交易所 (TWSE)** - 台股即時與歷史資料
- **證券櫃檯買賣中心 (TPEX)** - 上櫃股票資料
- **Alpha Vantage / Yahoo Finance** - 美股資料

請遵守各資料提供者的使用條款與限制。

## 📝 授權條款

本專案採用 [MIT License](LICENSE)

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 📧 聯絡方式

- 作者：Ocean Wu
- Email: 
- GitHub: 
- 問題回報：

## 🙏 致謝

感謝所有貢獻者和以下開源專案：

- [FastAPI](https://fastapi.tiangolo.com/)
- [React](https://react.dev/)
- [TA-Lib](https://ta-lib.org/)

---

**再次提醒：本軟體僅供教育用途，不構成投資建議。投資前請審慎評估風險。**
