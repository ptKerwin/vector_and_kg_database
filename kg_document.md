# RAG_with_knowledge_graph(Neo4j) 文件

## Neo4j

1. 專案簡介
   本專案結合 Retrieval-Augmented Generation (RAG) 與知識圖譜，利用 LangChain 生態系與 Neo4j 圖資料庫，實現結構化知識檢索與問答。資料來源以 Wikipedia 條目為例，經 LLM 處理後轉為圖譜，並支援自然語言查詢。

2. 技術與套件說明
   2.1 LangChain 套件
   langchain_core：提供流程控制（如 RunnableBranch、RunnableParallel）、資料結構（如 BaseModel）、提示模板（PromptTemplate）等基礎功能。
   langchain_community：整合外部資源，包含 Neo4jVector（向量資料庫）、Neo4jGraph（圖資料庫操作）。
   langchain_experimental：進階功能，如 LLMGraphTransformer，將文本轉為圖譜結構。
   langchain_openai / langchain_groq / langchain_huggingface：支援多種 LLM 與嵌入模型，分別對應 OpenAI、Groq、HuggingFace 等平台。
   2.2 Neo4j
   Neo4j 是一套高效能圖資料庫，適合儲存與查詢實體、關係等結構化知識。
   在本專案中，Neo4j 用於儲存 LLM 轉換後的知識圖譜，支援 Cypher 查詢語言進行複雜的關聯檢索。
3. 系統架構與資料流程
   練習資料取得與分割：利用 WikipediaLoader 取得條目，並用 TokenTextSplitter 切分為適合處理的段落。
   LLM 轉圖譜：透過 LLMGraphTransformer，將文本內容轉換為圖譜格式（nodes/edges）。
   圖譜寫入 Neo4j：以 Neo4jGraph 將圖譜資料寫入 Neo4j 資料庫。
   向量化與混合檢索：用 HuggingFaceEmbeddings 產生向量，Neo4jVector 支援向量與結構化混合查詢。
   問答流程（RAG）：結合 Retriever、PromptTemplate 與 LLM，根據用戶問題檢索相關知識並生成答案。
4. 關鍵程式碼與模組說明
   4.1 Entities 類別與實體抽取
   利用 pydantic 統一資料格式，方便 LLM 輸出結構化資訊。
   names 欄位儲存所有抽取到的人名、組織名等實體。
   4.2 Retriever 與查詢流程
   structured_retriever 會先用 LLM 抽取問題中的實體，再用 Cypher 查詢圖譜，取得相關結構化知識。
   vector_index.similarity_search 則用向量方式檢索相關文本，補足圖譜查詢的不足。
   4.3 LangChain 各模組協作
   PromptTemplate：定義 LLM 輸入格式。
   RunnableBranch / RunnableParallel：流程分支與多路並行，靈活組合檢索與生成。
   LLMGraphTransformer：將文本自動轉為圖譜，降低人工建模負擔。
   Neo4jGraph / Neo4jVector：分別負責圖譜資料的寫入/查詢與向量檢索。
5. LangChain 與 Neo4j 的整合重點
   LangChain 提供模組化、可組合的流程設計，讓 LLM、檢索、圖譜查詢等功能能無縫整合。
   Neo4j 作為知識圖譜的儲存與查詢核心，支援複雜的關聯檢索，並可與向量檢索混合運用，提升問答準確度與靈活性。

## langchain family
- langchain-core: contains simple, core abstractions that have emerged as a standard, as well as LangChain Expression Language as a way to compose these components together.
- langchain-community: contains all third party integrations.
- langchain: contains higher-level and use-case specific chains, agents, and retrieval algorithms that are at the core of the application's cognitive architecture.
