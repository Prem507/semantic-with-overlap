# semantic-with-overlap
📄 Advanced NLP – FAISS-based Semantic Document QA

A **Document Question Answering System** that retrieves relevant context from PDFs using  
**semantic embeddings + semantic chunking with overlap + FAISS vector search**.

---

## 🚀 Features

- 📥 Load and read multiple PDF documents  
- ✂️ Sentence-level splitting  
- 🧠 **Semantic chunking** (group by similarity)  
- 🔁 **Overlap between chunks** to preserve context  
- 🧠 Embeddings via **Sentence Transformers (all-MiniLM-L6-v2)**  
- ⚡ Fast retrieval using **FAISS (IndexFlatL2)**  
- 🔍 Returns **Top-K (3) most relevant chunks**

---

## 🛠️ Tech Stack

- Python  
- NLTK  
- Sentence Transformers  
- FAISS  
- NumPy  
- PyPDF2  

---

## ⚙️ How It Works

1. Load PDFs and extract text  
2. Split into sentences  
3. Generate **sentence embeddings**  
4. Create chunks:
   - If similarity between consecutive sentences > 0.7 → same chunk  
   - Else → new chunk  
   - Add **overlap (last sentence)** to next chunk  
5. Convert chunks → embeddings  
6. Store embeddings in **FAISS index**  
7. Convert query → embedding  
8. Retrieve **Top-K similar chunks** using FAISS  

---

## ▶️ Run

```bash
git clone https://github.com/Prem507/Advanced-NLP.git
cd Advanced-NLP
pip install nltk numpy faiss-cpu sentence-transformers PyPDF2
python main.py
💡 Example
Input

Ask Question: What is leave policy?
Output

Best Chunk Answers:

Answer:
Employees are entitled to leave as per company policy...
Distance Score: 0.42
--------------------------------
📈 Key Improvements
Keyword search → Semantic search (embeddings)
Fixed chunking → Semantic chunking
No context → Overlap chunking
Linear search → FAISS vector search (fast & scalable)
📈 Next Steps
Add LLM (OpenAI / Llama) → complete RAG system
Show source (page number, document name)
Build Streamlit UI
Use FAISS IndexIVF / HNSW for large-scale data
👨‍💻 Author
Prem Chandh
Aspiring Generative AI Engineer
GitHub: https://github.com/Prem507⁠�
⭐ Summary
This project demonstrates how to build a semantic retrieval system using FAISS, forming the foundation for real-world RAG-based AI applications.

---

A couple of small but worthwhile refinements in your code:

- `extract_text()` can return `None` → guard it:
  ```python
  if page_text:
      text += page_text
You’re using L2 distance in FAISS, so:
lower score = better match
(you might want to mention that in output)
For better retrieval later:
Python
faiss.normalize_L2(embeddings)
and use cosine similarity via inner product index
