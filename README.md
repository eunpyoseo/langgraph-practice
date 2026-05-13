# LangGraph 기반 멀티 에이전트 - 운동 추천 시스템

LangGraph를 공부하면서 만든 실습 프로젝트입니다.  
사용자의 증상을 분석해 맞춤 운동을 추천하는 멀티 에이전트 파이프라인을 구현했습니다.

---

## 🌟 주요 특징 (Multi-Agent System)

## 🤖 멀티 에이전트(Multi-Agent) 시스템이란?

**멀티 에이전트 시스템**은 하나의 거대한 언어 모델(LLM)이 모든 대답을 처리하는 기존 방식에서 벗어나, **각기 다른 전문 역할(Persona)을 부여받은 여러 AI 에이전트가 상태(State)를 공유하며 협력하여 복잡한 문제를 해결하는 아키텍처**입니다. 

본 프로젝트에서는 LangGraph를 활용해 파이프라인을 구축했으며, 사용자 질의가 들어오면 3개의 에이전트가 다음과 같이 데이터를 주고받으며 최종 리포트를 완성합니다.

### 🔄 각 에이전트별 역할 및 입출력(I/O) 예시

**[사용자의 최초 질문]**: *"체력이 안 좋고, 살이 계속 찌는데 어떤 운동을 할까?"*

#### 1. 증상 추출 에이전트 (Symptom Extraction Agent)
사용자의 일상적인 질문 속에서 의학적/신체적 '핵심 키워드'만을 정제하여 뽑아내는 역할을 합니다.
* **Input (입력)**: 사용자의 원본 질문 전체
* **Output (출력)**: 파악된 핵심 증상 키워드
  > `["체력 저하", "체중 증가 및 비만 관리 필요"]`

#### 2. 운동 후보 선정 에이전트 (Exercise Candidate Agent)
앞서 추출된 증상 키워드만 전달받아, 해당 증상 완화에 가장 효과적인 운동을 브레인스토밍하고 선정 근거를 마련합니다.
* **Input (입력)**: 추출 에이전트가 넘겨준 증상 키워드 리스트
* **Output (출력)**: 맞춤형 운동 리스트 및 기대 효과 (Raw Data 형태)
  > `스쿼트 (기초대사량 증가), 플랭크 (코어 강화), 자전거 타기 (관절 부담 없는 유산소)`

#### 3. 답변 생성 에이전트 (Response Generation Agent)
사용자의 최초 질문, 추출된 증상, 그리고 추천 운동 데이터를 모두 종합하여 최종 사용자가 읽기 편한 포맷(개조식 마크다운)으로 변환하고 교정합니다.
* **Input (입력)**: 이전 에이전트들이 생성한 모든 State 데이터 (질문 + 증상 + 운동 리스트)
* **Output (출력)**: 가독성이 극대화된 최종 마크다운 리포트
  > **[추천 운동]**
  > 1. **스쿼트**: 하체 근력 강화 및 신진대사 촉진으로...
  > 2. **플랭크**: 코어 근력 강화와 척추 안정성 향상에...
  > 3. **자전거 타기**: 관절에 무리 없이 유산소 운동을...
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
