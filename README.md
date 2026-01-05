# 自主學習評量助手 (Self-Directed Learning Assessment AI)

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![React](https://img.shields.io/badge/React-19.0-blue)
![Gemini API](https://img.shields.io/badge/Gemini-3.0%20Flash-orange)

## 📖 專案簡介 (Introduction)

**自主學習評量助手** 是一款專為台灣高中108課綱「自主學習」設計的 AI 輔助評量工具。旨在協助教師快速分析學生的自主學習成果，並提供學生具備「鷹架理論 (Scaffolding)」的引導式回饋。

本系統採用 Google 最新 **Gemini 3.0 Flash** 模型，具備**多模態 (Multimodal)** 分析能力。不僅能閱讀 PDF 中的純文字論述，更能**視覺化分析**文件中的圖表正確性、排版邏輯以及實作成品照片，提供比傳統純文字 AI 更精確的評量結果。

## ✨ 核心功能 (Key Features)

### 1. 多模態 AI 深度分析 (Multimodal Analysis)
系統不只「讀」文字，還會「看」圖片：
*   **文字語意分析**：理解邏輯論證、反思深度與科學方法。
*   **視覺圖表分析**：檢查數據圖表 (Charts) 的座標軸、單位與類型選擇是否正確。
*   **實作證據檢核**：辨識程式碼截圖、手繪草稿、實作成品照片，驗證歷程真實性。
*   **排版美學評估**：分析標題層級與閱讀舒適度。

### 2. 智慧採樣演算法 (Smart Page Sampling)
為了在有限的 AI Context Window 中提供最完整的分析，本系統內建 PDF 結構掃描引擎：
*   **全文提取**：無條件提取整份 PDF 的純文字內容。
*   **內容感知篩選 (Content-Aware Selection)**：
    *   **掃描階段**：計算每一頁的「視覺權重分數」(Visual Score)，偵測點陣圖片 (Photos) 與向量路徑 (Charts)。
    *   **決策階段**：強制鎖定**第 1 頁** (封面/摘要)，並自動挑選分數最高的 **Top 14 頁**。
    *   **結果**：即使檔案長達 50 頁，AI 也能精準鎖定包含關鍵圖表、實驗數據與成品照片的 **15 頁精華**進行視覺分析。

### 3. 智慧分類與評分規準 (Smart Classification & Rubrics)
自動判斷檔案類型，並套用專屬評分量表（1-5分制）：
*   **Category 1: 自然科學與實驗研究** (強調：實驗設計、數據視覺化、邏輯推論)
*   **Category 2: 社會人文與閱讀探究** (強調：議題洞察、文字流暢、學術規範)
*   **Category 3: 實作技能與專題開發** (強調：執行成果、問題解決、歷程紀錄)

### 4. 結構化回饋報告 (Structured Feedback)
*   **雷達圖 (Radar Chart)**：直觀呈現五大向度能力分佈。
*   **條列式優點與建議**：清晰列出具體亮點與改進方向。
*   **大學申請百字簡述**：AI 自動生成符合學習歷程檔案上傳需求的「百字簡述」範例。
*   **教師專區**：提供總結評語與學術倫理（抄襲/引用）風險檢核。

### 5. PDF 報告輸出
*   支援一鍵下載完整評量報告 (PDF 格式)，方便師生存檔或列印。

## 🛠️ 技術架構 (Tech Stack)

*   **Frontend**: React 19, TypeScript, Tailwind CSS
*   **AI Model**: Google Gemini 3.0 Flash Preview (`gemini-3-flash-preview`) via `@google/genai` SDK
*   **PDF Processing**: 
    *   `pdfjs-dist`: 用於提取純文字與渲染頁面為圖片 (Canvas rendering)。
    *   `html2pdf.js`: 用於將網頁報告輸出為 PDF 檔案。
*   **Visualization**: Recharts (Radar Chart)
*   **Icons**: Lucide React

## 🚀 本地安裝與執行 (Getting Started)

### 前置需求
*   Node.js (v18+)
*   Google Gemini API Key (需至 [Google AI Studio](https://aistudio.google.com/) 申請)

### 安裝步驟

1.  **Clone 專案**
    ```bash
    git clone https://github.com/AvatarBiology/sdl-helper.git
    cd self-directed-learning-ai
    ```

2.  **安裝依賴**
    ```bash
    npm install
    ```

3.  **設定環境變數**
    在專案根目錄建立 `.env` 檔案，並填入您的 API Key：
    ```env
    API_KEY=your_gemini_api_key_here
    ```

4.  **啟動開發伺服器**
    ```bash
    npm start
    # 或
    npm run dev
    ```

5.  **開始使用**
    打開瀏覽器前往 `http://localhost:1234` (或終端機顯示的 Port)。

## 📝 使用說明 (Usage)

1.  **上傳檔案**：點擊首頁上傳區，選擇一份 PDF 格式的自主學習檔案（建議包含圖表或照片以發揮最大分析效能）。
2.  **等待分析**：系統會提取所有文字，並智慧挑選前 **15 頁**具備高度視覺價值的頁面傳送至 Gemini。
3.  **檢視報告**：
    *   查看雷達圖了解強弱項。
    *   閱讀「具體建議」來優化檔案。
    *   參考「百字簡述」修改上傳至教育部的簡述文字。
4.  **下載/重置**：點擊右上角「下載 PDF 報告」保存結果，或點擊「重新評量」測試下一份檔案。

## 🤝 貢獻與版權 (Contribution & License)

*   本專案採 MIT License 開源。
*   評分規準參考台灣 108 課綱自主學習核心素養設計。
*   **Disclaimer**: AI 評量結果僅供輔助參考，正式成績應以授課教師評分為準。

---
Developed with ❤️ for Education.
