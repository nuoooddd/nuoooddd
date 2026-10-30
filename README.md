# nuo

Software Engineering, Class of 2027 — looking for **AI Agent / LLM backend** roles.

软件工程本科 · 2027 届 · 求职方向 **AI Agent / 大模型应用后端开发**

主要写 Python 和 Java，最近在做的一个 RAG 项目放在下面。

## kb-agent — RAG 知识库问答服务

Python / FastAPI，2026.09 至今。切分、检索、生成、引用、评测都自己写，没用向量数据库，也没上 LangChain。

- **切分**：递归切分，chunk_size 500 字 / overlap 80 字。分隔符按 `\n\n` → `\n` → 句号 → 问号感叹号分号 → 逗号 → 字符逐级回退，保证块不超长。13 篇文档切出 62 块，平均 487 字
- **分词**：中文按单字 + 相邻二元组切，不依赖 jieba。BM25 用 k1=1.5、b=0.75
- **检索**：余弦相似度与 BM25 两路，各自 min-max 归一化后加权融合。alpha 做过对照实验（纯 BM25 / 混合 / 纯向量），Recall@1 分别是 75.0% / 92.5% / 85.0%，取 0.6
- **拒答**：融合分归一化后每批最高分恒为 1.0，拿它比阈值永远为真，所以改成比归一化前的原始余弦，低于 0.52 直接短路、不调模型
- **Agent**：Function Calling 循环，最多 5 轮，工具是知识检索；会话记忆用滑动窗口按轮次淘汰
- **评估**：自建 50 条题，25 条字面、15 条同义改写、10 条库里没有答案。当前 Recall@1 92.5%、MRR 0.958，10 条不可答全部拒答
- **MCP**：手写 JSON-RPC 2.0 over stdio，零依赖，暴露 `search_knowledge` 和 `ask_knowledge_base` 两个工具

上面的数字跑 `python -m app.eval` 可复现。

## 技术栈

Python、Java、SQL / FastAPI、Spring Boot、Spring Security + JWT、MyBatis / MySQL、Redis / Git、Maven

## 联系

邮箱：Yukari_nuo@163.com
