# 🔬 T4(구조 차용) vs T5(독자 설계) 기술적 판별 기준
> **Technical Criteria for Distinguishing Adopted vs Native Architectures**

같은 "자체 학습(Pre-training)" 모델이라도, 엔지니어링 깊이에 따라 T4와 T5는 명확히 구분됩니다.
마케팅 용어에 현혹되지 않고, **코드와 구조(Code & Structure)**를 통해 등급을 판별하는 4가지 기준을 제시합니다.

---

## 1. 변경의 본질: Config 튜닝인가, Topology 재설계인가? (Nature of Change)
**"건물을 증축(Scaling)했는가, 공법을 새로 설계(Architecting)했는가?"**

가장 본질적인 차이는 변화가 **정량적(Quantitative)**이냐 **정성적(Qualitative)**이냐에 있습니다.

### **T4-2 (양적 변형 - Scaling)**
* **상세:** `config.json` 파일 내의 Hyperparameter 수치만 조정합니다.
    * `num_hidden_layers`: 32 → 48 (깊이 확장)
    * `hidden_size`: 4096 → 5120 (용량 확장)
    * `num_attention_heads`: 32 → 40 (병렬 처리 확장)
* **기술적 함의:** 30층 아파트를 설계도 그대로 50층으로 증축하는 것과 같습니다. 건물의 하중을 견디는 공법이나 내부 배관 구조(Data Flow)는 원본(Llama 등)과 동일합니다.

### **T5 (질적 변형 - Architecting)**
* **상세:** 모델의 **연산 그래프(Computational Graph)**와 **토폴로지(Topology)** 자체를 변경합니다.
    * **Attention 메커니즘 교체:** 예) MHA(Multi-Head) → MLA(Multi-Latent) 또는 Sliding Window Attention 도입.
    * **Normalization 위치 변경:** Pre-Norm → Post-Norm 또는 RMSNorm 수식 변경.
    * **Activation 함수 재정의:** GeLU → SwiGLU 등 연산 효율이 다른 함수로 교체.
* **기술적 함의:** 데이터가 입력되어 출력될 때까지의 **'계산 경로'와 '정보 흐름'**을 재설계한 것입니다. 이는 아파트가 아니라, 전혀 새로운 공법으로 '돔 구장'을 짓는 것과 같습니다.

---

## 2. 구현의 깊이: 코드 호환성 vs 독립성 (Implementation Depth)
**"표준 생태계에 얹혀 가는가, 독자 노선을 걷는가?"**

### **T4 (플랫폼 종속형 / Standard)**
* **판별법:** HuggingFace의 표준 클래스(`AutoModelForCausalLM`)로 별도 옵션 없이 바로 로딩됩니다.
* **코드 구조:** `modeling_llama.py` 등 공개된 표준 라이브러리를 그대로 상속받습니다.
* **의미:** 유지보수가 쉽고 생태계 도구(Quantization, Serving)와 즉시 호환되지만, 원본 아키텍처의 취약점과 리스크도 그대로 상속받습니다.

### **T5 (코드 독립형 / Custom)**
* **판별법:** `trust_remote_code=True` 옵션을 켜지 않으면 모델이 로드되지 않습니다.
* **코드 구조:** 모델 저장소 안에 `modeling_custom.py`와 같은 독자적인 파이썬 코드가 포함되어 있으며, 이를 통해 계산 그래프를 직접 정의합니다.
* **의미:** 표준 생태계와 단절되는 불편함을 감수하고서라도, **극한의 성능 최적화나 특수 목적(보안 등)을 위해 설계를 뜯어고쳤음**을 의미합니다.

---

## 3. 언어 기관: 확장(Expansion) vs 원천 구축(Native)
토크나이저(Tokenizer)는 AI가 세상을 보는 '해상도'입니다.

### **T4 (확장형 - Vocabulary Expansion)**
* **방식:** Llama 3 토크나이저(약 12.8만 개) 뒤에 한국어 단어 3~5만 개를 덧붙입니다.
* **한계:** 기존 영어 토큰이 메인이고 한국어는 '셋방살이'입니다. 한국어 처리 효율이 떨어져 토큰 소모량이 많습니다.

### **T5 (원천형 - Native Construction)**
* **방식:** 기존 것을 버리고, 한국어 코퍼스를 기반으로 처음부터(From Scratch) 단어 사전을 만듭니다.
* **효과 (TCO 절감):**
    * *예문: "아버지가방에들어가신다"*
    * **T4:** [아, 버, 지, 가, 방, 에...] (6~7 토큰 소모)
    * **T5:** [아버지, 가방, 에, 들어가신다] (3~4 토큰 소모)
    * **결과:** 같은 내용을 처리할 때 **추론 비용(Inference Cost)이 30% 이상 절감**됩니다.

---

## 4. 지식의 기원: 증류(Distillation) vs 원천 학습(Organic)

### **T4 (지식 증류 의존)**
* **방식:** GPT-4나 Claude가 생성한 데이터(Synthetic Data)를 학습합니다.
* **위험성:** Teacher 모델의 편향을 그대로 물려받는 **'Degraded Copy(열화된 복제)'**가 될 위험이 있습니다.

### **T5 (원천 데이터 학습)**
* **방식:** 인간이 만든 원천 데이터(Raw Text)의 통계적 패턴을 스스로 학습합니다.
* **가치:** 비용이 수십 배 더 들지만, 이를 통해서만 **진정한 의미의 '고유한 지능'과 '문화적 주권'**이 확보됩니다.
