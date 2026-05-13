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

![LangGraph Structure](./images/graph_structure.png)

> **진행 순서**: `START` → `추출 에이전트` → `후보 에이전트` → `답변 생성 에이전트` → `END`

---

## 🖥 실행 결과 (Example Results)

**질문 예시**: "체력이 안 좋고, 살이 계속 찌는데 어떤 운동을 할까?"

각 에이전트의 파이프라인을 거쳐 출력된 최종 결과물입니다.

![Execution Result](./images/result_sample.png)

### **출력 샘플**
* **[증상]**: 체력 저하, 체중 증가 관리 필요
* **[추천 운동]**: 
    1. **스쿼트**: 하체 근력 강화 및 신진대사 촉진으로 체력 향상과 기초대사량 증가에 효과적입니다.
    2. **플랭크**: 코어 근력 강화와 척추 안정성 향상에 도움을 주어 전반적인 자세 개선에 좋습니다.
    3. **자전거 타기**: 관절에 무리 없이 유산소 운동을 진행할 수 있어 체지방 연소에 탁월합니다.

---

## 🚀 시작하기

1.  **Ollama 설치**: [Ollama 공식 홈페이지](https://ollama.com/)에서 설치 후 로컬 모델을 실행합니다.
    ```bash
    ollama run llama3.2
    ```
2.  **필수 패키지 설치**:
    ```bash
    pip install langgraph langchain_community langchain_openai
    ```
3.  **코드 실행**: `langgraph-practice.ipynb` 파일을 열고 환경 변수 설정 없이 로컬 베이스 경로(`http://localhost:11434/v1`)를 통해 실습을 진행합니다.
