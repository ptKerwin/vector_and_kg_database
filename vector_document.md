# 技術文件：RAG 與 ChromaDB 向量資料庫整合

1. 專案簡介
   本專案展示如何結合 Retrieval-Augmented Generation (RAG) 與 ChromaDB 向量資料庫，利用 LangChain 生態系進行文件檢索與問答。以 PDF 文件為例，將內容分割、向量化後存入 ChromaDB，並透過 LLM 回答用戶問題。

2. 技術與套件說明
   2.1 LangChain 套件
   langchain_core：提供流程控制（如 RunnableAssign）、提示模板（ChatPromptTemplate）、輸出解析（StrOutputParser）等基礎功能。
   langchain_community：支援文件載入（如 PyPDFLoader）。
   langchain_groq：串接 Groq LLM，作為問答生成模型。
   2.2 ChromaDB
   ChromaDB：高效能的本地向量資料庫，支援文件向量化儲存與相似度查詢。
   HuggingFaceEmbeddingFunction：用於將文本轉換為向量，支援多種 HuggingFace 模型。
   2.3 其他依賴
   PyPDFLoader：載入 PDF 文件內容。
   rich：美化終端輸出。
3. 系統架構與資料流程
   文件載入與分割

使用 PyPDFLoader 讀取 PDF 文件內容。
透過 RecursiveCharacterTextSplitter 將長文本切分為多個 chunk。
向量化與資料寫入 ChromaDB

使用 HuggingFaceEmbeddingFunction 將每個 chunk 轉為向量。
將向量與原始文本存入 ChromaDB collection。
查詢與檢索流程

用戶輸入問題時，將問題向量化並查詢 ChromaDB，取得最相關的文件片段。
問答生成流程

將檢索到的內容與用戶問題一同送入 LLM，生成最終回答。 4. 關鍵程式碼與模組說明
4.1 文件載入與分割
4.2 向量化與資料寫入
4.3 檢索方法（retrieve_vstore）
4.4 LangChain chain 組合與問答流程 5. LangChain 與 ChromaDB 的整合重點
LangChain 提供模組化流程設計，讓文件檢索、向量查詢、LLM 問答能無縫串接。
ChromaDB 作為本地向量資料庫，支援高效的相似度查詢，提升問答準確度。
HuggingFaceEmbeddingFunction 讓向量化流程靈活可換模型，適應不同語言任務。 6. 常見問題與錯誤排查
ChromaDB 查詢無結果：請確認文件已正確寫入，查詢文本有意義。
LLM 回答不準確：可調整檢索 chunk 數量、嵌入模型或 prompt 設計。
PDF 讀取失敗：檢查檔案路徑與格式。
