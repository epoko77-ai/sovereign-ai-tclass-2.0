# 🔬 T4(구조 차용) vs T5(독자 설계) 기술적 판별 기준
> **Technical Criteria for Distinguishing Adopted vs Native Architectures**

같은 "자체 학습(Pre-training)" 모델이라도, 엔지니어링의 깊이에 따라 **T4(Architecture Scaler)**와 **T5(Native Architecture)**는 명확히 구분됩니다.

마케팅 용어에 현혹되지 않고, **코드(Code)와 구조(Structure)**라는 엔지니어링 실체를 통해 등급을 판별하는 4가지 기준을 제시합니다.

---

## 1. 변경의 본질: Config 튜닝인가, Topology 재설계인가? (Nature of Change)
**"건물을 증축(Scaling)했는가, 공법을 새로 설계(Architecting)했는가?"**

가장 본질적인 차이는 변화가 **정량적(Quantitative)**이냐 **정성적(Qualitative)**이냐에 있습니다.

### **T4-2 (양적 변형 - Scaling)**
* **상세:** `config.json` 파일 내의 Hyperparameter 수치만 조정합니다.
  * `num_hidden_layers`: 32 → 48 (깊이 확장)
  * `hidden_size`: 4096 → 5120 (용량 확장)
  * `num_attention_heads`: 32 → 40 (병렬 처리 확장)
* **기술적 함의:** 30층 아파트를 설계도 그대로 50층으로 증축하는 것과 같습니다. 건물의 하중을 견디는 공법이나 내부 배관 구조(Data Flow)는 원본(Llama, Mistral 등)과 동일합니다.

### **T5 (질적 변형 - Architecting)**
* **상세:** 모델의 **연산 그래프(Computational Graph)**와 **토폴로지(Topology)** 자체를 변경합니다.
  * **Attention 메커니즘 교체:** 예) MHA(Multi-Head) → MLA(Multi-Latent) 또는 Sliding Window Attention 도입.
  * **Normalization 위치 변경:** Pre-Norm(입력 전 제어) → Post-Norm(출력 후 제어) 또는 수식 변경.
  * **Activation 함수 재정의:** GeLU → SwiGLU 등 연산 효율이 다른 함수로 교체.
* **기술적 함의:** 데이터가 입력되어 출력될 때까지의 **'계산 경로'와 '정보 흐름'**을 재설계한 것입니다. 이는 증축이 아니라, 새로운 공법을 적용해 짓는 것과 같습니다. 파라미터 수가 같아도 정보가 섞이고, 안정화되고, 증폭되는 메커니즘 자체가 다릅니다.

---

## 2. 구현의 깊이: 코드 호환성 vs 독립성 (Implementation Depth)
**"표준 생태계에 얹혀 가는가, 독자 노선을 걷는가?"**

### **T4 (플랫폼 종속형 / Standard)**
* **판별법:** HuggingFace의 표준 클래스(`AutoModelForCausalLM`)로 별도 옵션 없이 바로 로딩됩니다.
* **코드 구조:** `modeling_llama.py` 등 공개된 표준 라이브러리를 그대로 상속받습니다. 핵심 연산 로직(Attention → Residual → MLP)과 변수명이 원본과 유사합니다.
* **리스크:** 원본 아키텍처의 취약점이나 라이선스 이슈가 발생했을 때, 기술적 커플링(Coupling)으로 인해 그 리스크를 그대로 상속받습니다.

### **T5 (코드 독립형 / Custom)**
* **판별법:** `trust_remote_code=True` 옵션을 켜지 않으면 모델이 로드되지 않습니다.
* **코드 구조:** 모델 저장소 안에 `modeling_custom.py`와 같은 독자적인 파이썬 코드가 포함되어 있으며, 이를 통해 계산 그래프를 직접 정의합니다.
* **가치:** 표준 생태계와 단절되는 불편함을 감수하고서라도, **극한의 성능 최적화나 특수 목적(보안 등)을 위해 설계를 뜯어고쳤음**을 의미합니다. 외부 생태계의 변화와 무관하게 생존 가능한 진정한 기술적 독립 상태입니다.

---

## 3. 언어 기관: 확장(Expansion) vs 원천 구축(Native)
토크나이저(Tokenizer)는 AI가 세상을 보는 '눈'입니다. 이 눈을 어떻게 만들었는가가 한국어 처리 효율을 좌우합니다.

### **T4 (확장형 - Vocabulary Expansion)**
* **방식:** 기존 모델(Llama 2/3 등)의 토크나이저를 베이스로 삼고, 뒤에 한국어 단어 수만 개를 덧붙입니다.
* **한계:** 영어 중심의 임베딩 공간(Embedding Space) 구석에 한국어를 '셋방살이' 시키는 구조입니다. 한국어 문장의 압축률(Compression Rate)이 떨어져, 같은 말을 해도 더 많은 토큰을 소모합니다. 이는 곧 **운영 비용(TCO) 증가**로 이어집니다.

### **T5 (원천형 - Native Construction)**
* **방식:** 기존 것을 버리고, 무작위 초기화(Random Initialization) 상태에서 한국어 코퍼스를 기반으로 처음부터(From Scratch) 학습시킵니다.
* **효과:** 한국어의 교착어적 특성(조사, 어미 분리)을 완벽히 반영합니다.
  * *예문: "아버지가방에들어가신다"*
  * **T4:** [아, 버, 지, 가, 방, 에...] (6~7 토큰 소모)
  * **T5:** [아버지, 가방, 에, 들어가신다] (3~4 토큰 소모)
  * **결과:** **추론 비용(Inference Cost)이 30% 이상 절감**되며, 데이터 처리의 주권을 확보합니다.

---

## 4. 지식의 기원: 증류(Distillation) vs 원천 학습(Organic)

### **T4 (지식 증류 의존)**
* **방식:** GPT-4나 Claude 같은 Teacher 모델이 생성한 합성 데이터(Synthetic Data)나 출력 확률(Logits)을 학습합니다.
* **위험성:** 효율적일지는 몰라도, 상위 모델의 편향과 논리 구조를 그대로 답습하는 **'Degraded Copy(열화된 복제)'**가 될 위험이 큽니다.

### **T5 (원천 데이터 학습)**
* **방식:** 타사의 지식을 빌리지 않고, 직접 큐레이션한 원천 데이터(Raw Corpora)의 통계적 패턴을 스스로 학습합니다.
* **가치:** 시간과 비용이 수십 배 더 들지만, 이를 통해서만 우리의 문화적 맥락(Context)과 가치관이 내재화된 **'고유한 지능'**을 확보할 수 있습니다.

---

## ✅ [요약] T4 vs T5 기술 비교표

| 비교 항목 | T4 (Adopted / Scaler) | T5 (Native Architecture) |
| :--- | :--- | :--- |
| **설계 본질** | 양적 확장 (Config 튜닝) | **질적 재설계 (Topology 변경)** |
| **코드 의존성** | HuggingFace 표준 라이브러리 종속 | **독자 모델링 코드 (Custom Code)** |
| **로드 옵션** | `AutoModel` 자동 로드 | `trust_remote_code=True` 필수 |
| **토크나이저** | 영어 베이스 + 한국어 추가 (확장) | **한국어 중심 처음부터 학습 (Native)** |
| **지식 원천** | 지식 증류 (Distillation) 위주 | **원천 데이터 (Raw Corpora) 위주** |
| **핵심 가치** | 효율성, 호환성, 빠른 개발 | **기술 주권, 최적화, 보안성** |

---

## 📝 [자가 진단] 판별 문진표 (Checklist)
내 모델이 진정한 주권(Sovereign) 모델인지 확인하려면 다음 4가지 질문에 답해보십시오.

1. **(Topology)** 블록 내부의 연산 흐름과 구조 자체를 재설계했습니까? (Yes/No)
2. **(Code)** 호환되지 않는 독자적인 모델링 클래스(Class)를 새로 짰습니까? (Yes/No)
3. **(Tokenizer)** 영어 토크나이저에 한국어를 덧붙인 것이 아니라, 처음부터 새로 만들었습니까? (Yes/No)
4. **(Data)** 타사 모델의 답변을 증류(Distillation)하여 배운 것이 아니라, 원천 데이터로 학습했습니까? (Yes/No)

> **결과 판정:** 위 질문에 모두 **"Yes"**라면, 당신의 모델은 **T5 Native Architecture** 등급입니다.
