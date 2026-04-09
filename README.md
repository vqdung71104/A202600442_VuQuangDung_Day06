# 2A202600217-NguyenTienDat-Day06

**Họ tên:** Vũ Quang Dũng  
**MSSV:** 2A202600442
**Track:** Vinmec  
**Project:** VinmecPrep AI — Chatbot hỗ trợ bệnh nhân chuẩn bị trước khi khám

---

## Về project

VinmecPrep AI là working prototype chatbot giúp bệnh nhân:
- Biết cần chuẩn bị gì trước buổi khám (nhịn ăn, giấy tờ, đặt lịch)
- Nhận checklist cá nhân hoá theo từng chuyên khoa
- Tìm cơ sở Vinmec gần nhất kèm địa chỉ, hotline, giờ làm việc

Stack: **LangGraph ReAct Agent** · **FastAPI** · **Kafka + Redis Streams** · **Weaviate RAG** · **LiteLLM** (Groq / vLLM) · **SearXNG** · **Docker Compose**

**→ Repo nhóm:** https://github.com/Quyenm/Nhom26-E403-Day06

---

## Architecture

![Architecture](extras/architecture.png)

Flow tổng quát:

```
User Input
    │
    ▼
Guardrails (5 lớp)          ← src/guardrails.py
    │ PASS
    ▼
FastAPI /chat
    │
    ▼
Kafka Producer ──► Topic: vinmec.chat.jobs
                        │
                        ▼
                  Kafka Consumer
                        │
                        ▼
              LangGraph ReAct Agent
              ┌─────────────────────┐
              │  RAG (Weaviate)     │
              │  Web Search         │
              │  Hospital Finder    │
              └─────────────────────┘
                        │
                        ▼
                Redis (result cache)
                        │
                        ▼
              FastAPI poll → Response
```

---



*VinUni A20 — AI Thực Chiến · Day 06 · 09/04/2026*