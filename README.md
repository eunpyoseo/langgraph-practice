# LangGraph 기반 멀티 에이전트 - 운동 추천 시스템

LangGraph를 공부하면서 만든 실습 프로젝트입니다.  
사용자의 증상을 분석해 맞춤 운동을 추천하는 멀티 에이전트 파이프라인을 구현했습니다.

---

## 🌟 주요 특징 (Multi-Agent System)

단일 LLM 호출 방식에서 벗어나, 3개의 독립적인 에이전트가 상태(State)를 공유하며 순차적으로 작업을 수행하도록 설계했습니다.

1.  **증상 추출 에이전트 (Symptom Extraction Agent)**: 사용자의 복합적인 질문에서 핵심 신체 증상을 파악하여 추출합니다.
2.  **운동 후보 선정 에이전트 (Exercise Candidate Agent)**: 추출된 증상을 기반으로 해결 가능한 운동 리스트를 선별합니다.
3.  **답변 생성 에이전트 (Response Generation Agent)**: 최종적으로 사용자가 읽기 편한 개조식(Bullet points) 형태의 리포트로 답변을 포맷팅합니다.

---

## 🛠 기술 스택 (Tech Stack)

| 구분 | 기술 |
| :--- | :--- |
| **Framework** | LangChain, LangGraph |
| **LLM (Local)** | Ollama (Llama 3.2 등) |
| **Language** | Python 3 |
| **Environment** | Jupyter Notebook (.ipynb) |

---

## 📊 워크플로우 구조 (Workflow Structure)

LangGraph의 `StateGraph`를 활용하여 에이전트 간의 제어 흐름(Control Flow)을 설계했습니다.

<img width="130" height="514" alt="graph_structure" src="https://github.com/user-attachments/assets/106ad190-fd92-4b6b-bcd0-45326eb73a25" />

> **진행 순서**: `START` → `추출 에이전트` → `후보 에이전트` → `답변 생성 에이전트` → `END`

---

## 🖥 실행 결과 (Example Results)

**질문 예시**: "체력이 안 좋고, 살이 계속 찌는데 어떤 운동을 할까?"

각 에이전트의 파이프라인을 거쳐 출력된 최종 결과물입니다.
<img width="1165" height="243" alt="result_sample" src="https://github.com/user-attachments/assets/a614130c-6ed8-4839-91ca-b9055659f7cf" />


---

## 🚀 시작하기

1. **Ollama 설치**: [Ollama 공식 홈페이지](https://ollama.com/)에서 설치 후 로컬 모델을 실행합니다.
    ```bash
    ollama pull exaone3.5:2.4b
    ```
2. **필수 패키지 설치**:
    ```bash
    pip install langgraph langchain langchain-community
    ```
3. **코드 실행**: `langgraph-practice.ipynb` 파일을 열고 순서대로 셀을 실행합니다.
