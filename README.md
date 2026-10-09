# Medical Assistant — RAG-Based Medical Question Answering

![Courses](https://img.shields.io/badge/Courses-Generative%20AI%20%2B%20NLP%20with%20GenAI-6f42c1)
![Grade](https://img.shields.io/badge/Grade-A%2B%20(4.33)-success)
![Type](https://img.shields.io/badge/Type-RAG%20%C2%B7%20LLM%20%C2%B7%20Vector%20Search-blue)
![Tools](https://img.shields.io/badge/Tools-LangChain%20%C2%B7%20Embeddings%20%C2%B7%20Vector%20DB-orange)

> **Cross-course project** — this single capstone-style build satisfies **both** the *Introduction to Generative AI* course and the *Natural Language Processing with Generative AI* course, because it is a retrieval-augmented generation system built on a large text corpus. The two courses are deliberately combined in this repository.

A retrieval-augmented generation (**RAG**) chatbot that answers medical questions using a trusted medical manual as its knowledge source, rather than relying on the language model's memory alone.

---

## Business Problem

Healthcare professionals face information overload — huge volumes of medical data combined with a need for quick, reliable answers, especially in emergencies. Generic AI models can **hallucinate**, which is unacceptable in a clinical setting. The solution is to ground the model's answers in an authoritative reference.

## Objective

Develop a RAG-based AI solution using renowned medical manuals to address information overload, streamline decision-making, and demonstrate a working prototype.

## Data

**The Merck Manual of Diagnosis & Therapy, 19th Edition** — a PDF of **4,114 pages** divided into 23 sections covering disorders, tests, diagnoses and drugs.

## Approach

1. **Baseline LLM** — first asked the questions directly to a large language model, to establish what an ungrounded model produces.
2. **Prompt engineering** — tested structured prompting to improve answer format and clarity.
3. **Data preparation** — loaded all 4,114 pages, cleaned and filtered them down to **4,111 usable pages**, then chunked the text into **17,219 chunks**.
4. **Embedding & vector database** — converted every chunk into vector embeddings and stored all 17,219 chunks in a vector database for semantic search.
5. **Retriever** — built a retriever that fetches the most relevant chunks for a question (typically the top 3).
6. **Prompt template** — designed a system + user prompt template that supplies the retrieved context and instructs the model to answer **only from that context**, in a clear structure.
7. **RAG answer function** — wired retrieval and generation together into a single response function.
8. **Experimentation** — compared four configurations: baseline balanced RAG, smaller retrieved context, larger retrieved context, and higher temperature.
9. **Evaluation** — scored answers on **groundedness** (is the answer supported by the retrieved context?) and **relevance** (does it answer the question?) on a 1–5 scale, with written justification.

## Question Types Covered

| # | Query type | Example question |
|---|---|---|
| 1 | Diagnostic assistance | Protocol for managing sepsis in a critical care unit |
| 2 | Disease information | Common symptoms of appendicitis and whether it can be cured |
| 3 | Emergency treatment | Effective treatments for sudden pain |
| 4 | Trauma care | Treatments for a person who sustained a physical injury |
| 5 | Precautions | Necessary precautions and treatment steps |

## Key Findings

- The RAG system **answered all five target question types** — diagnostic assistance, drug information, treatment plans, specialty knowledge and critical-care protocols.
- Grounded answers scored **5/5 on groundedness and 5/5 on relevance** across the evaluated questions, with no unsupported or weakly supported points flagged.
- **Retrieval size is a real trade-off** — fewer chunks improve focus, more chunks improve completeness; the balanced default performed best overall.
- **Grounding the model in the manual eliminated the hallucination risk** that the ungrounded baseline carried.

## Recommendations

1. Use **RAG rather than a plain LLM** for any clinical or other high-stakes knowledge task — grounding is what makes the output trustworthy.
2. Keep the retrieval configuration **balanced by default**, and tune chunk count per question type.
3. Always evaluate with **groundedness and relevance scoring** before deploying, and keep a **human in the loop** for clinical decisions.

## Skills Demonstrated

Large language models · prompt engineering · document loading and cleaning · text chunking · embeddings · vector databases · semantic retrieval · RAG architecture · systematic LLM output evaluation.

## Repository Structure

```
├── notebooks/
│   └── medical_assistant_rag_notebook.html   # full notebook (exported)
├── screenshots/
│   └── notebook_page_01.png … notebook_page_20.png
└── README.md
```

## Notebook Walkthrough

| Stage | Screenshot |
|---|---|
| Problem statement, business context & objective | `screenshots/notebook_page_01.png` |
| Baseline LLM, prompt engineering, data chunking | `screenshots/notebook_page_06.png` |
| Embeddings, vector store & retriever | `screenshots/notebook_page_11.png` |
| RAG answers & evaluation | `screenshots/notebook_page_16.png` |
| Insights & recommendations | `screenshots/notebook_page_20.png` |

---

*PGP in Data Science & Business Analytics · Great Lakes Executive Learning / The University of Texas at Austin, McCombs School of Business. Content drawn from the project notebook and course transcript.*
