# LangGraph 기반 멀티 에이전트 - 운동 추천 시스템

LangGraph를 공부하면서 만든 실습 프로젝트입니다.  
사용자의 증상을 분석해 맞춤 운동을 추천하는 멀티 에이전트 파이프라인을 구현했습니다.

---

## 🤖 멀티 에이전트 시스템 상세 설계 (Agent Design)

기존의 단일 LLM 호출 방식에서 벗어나, 역할을 분리한 3개의 에이전트가 `AgentState`를 공유하며 협력하도록 설계했습니다.  
각 에이전트의 상세 역할과 입/출력 흐름은 다음과 같습니다.

| 에이전트명 | 주요 역할 (Role) | 입력 예시 (Input) | 출력 예시 (Output) |
| :--- | :--- | :--- | :--- |
| **증상 추출** | 자연어 질문에서 핵심 신체 증상 정제 및 구조화 | "체력이 안 좋고 자꾸 살이 쪄요" | `["체력 저하", "체중 증가"]` |
| **운동 후보 선정** | 증상 기반 맞춤형 운동 브레인스토밍 및 선별 | `["체력 저하", "체중 증가"]` | `스쿼트, 플랭크, 자전거 등` |
| **답변 생성** | 취합된 모든 데이터를 종합하여 최종 리포트 작성 | 질문 + 증상 + 운동 리스트 | 마크다운 형식의 최종 리포트 |

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

**사용자 입력 (Query)**:  
> *"체력이 안 좋고, 살이 계속 찌는데 어떤 운동을 할까?"*

파이프라인을 거쳐 포맷팅 노드에서 최종적으로 출력된 결과물입니다.

<img width="1165" height="243" alt="result_sample" src="https://github.com/user-attachments/assets/a614130c-6ed8-4839-91ca-b9055659f7cf" />

### 💡 텍스트 출력 샘플
> **[파악된 증상]**
> * 체력 저하
> * 체중 증가 관리 필요
> 
> **[맞춤 추천 운동]**
> 1. **스쿼트**: 하체 근력 강화 및 신진대사 촉진으로 체력 향상과 기초대사량 증가에 효과적입니다.
> 2. **플랭크**: 코어 근력 강화와 척추 안정성 향상에 도움을 주어 전반적인 자세 개선에 좋습니다.
> 3. **자전거 타기**: 관절에 무리 없이 유산소 운동을 진행할 수 있어 체지방 연소에 탁월합니다.
> 4. 
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
