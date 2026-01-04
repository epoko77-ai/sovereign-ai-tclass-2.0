# ⚠️ 제2구간: 과도기 단계 (The Transitional Phase)
> **"기술을 빌려와 내재화를 시도하는 단계 (License Dependency)"**

이 구간은 오픈소스(Open Source) 생태계를 활용하여, 천문학적인 사전학습(Pre-training) 비용을 절감하면서도 자국어 성능을 확보하려는 실용적 접근 단계입니다.
그러나 **모델의 '두뇌(Base Model)'가 타인의 자산**이므로, 법적 종속성과 기술적 한계가 명확히 존재합니다.

---

## T2. 오픈소스 튜닝 및 CPT (Open-Source Tuning & CPT)
**"남의 뇌(Base Model)에 나의 지식을 주입하는 단계"**

### 1. 기술적 정의 (Technical Methodology)
Llama 3, Qwen 2.5, Mistral 등 가중치(Weights)가 공개된 모델을 베이스로 삼아 추가 학습을 수행한 형태입니다. 학습의 깊이에 따라 크게 두 가지로 나뉩니다.

* **Type A: SFT (Supervised Fine-Tuning):**
    * 베이스 모델에 질문-답변(Q&A) 쌍을 학습시켜 **말투와 지시 이행 능력(Instruction Following)**만 교정한 경우입니다.
    * 새로운 지식을 주입하기보다는, 모델이 이미 알고 있는 지식을 잘 꺼내 쓰도록 '행동 양식'만 튜닝한 수준입니다.
* **Type B: CPT (Continual Pre-training):**
    * 수백억 토큰 이상의 한국어 텍스트(뉴스, 백과사전 등)를 비지도 학습(Unsupervised Learning)으로 주입하여, 언어 이해 능력 자체를 보강한 경우입니다.
    * 모델의 파라미터 분포가 원본과 유의미하게 달라지지만, 여전히 기반 구조는 원본에 종속됩니다.

### 2. 소버린 관점의 분석 (Sovereign Analysis)
* **주권 수준:** 🔸 **Low (하)** - 기능적 주권은 일부 확보했으나, 원천 주권 부재.
* **치명적 리스크 1: 라이선스 종속 (License Contagion)**
    * 모델의 뿌리가 되는 Base Model의 라이선스 정책을 100% 승계해야 합니다.
    * *예: "월간 사용자 7억 명 이상 시 별도 라이선스 계약 필요" (Llama Community License)*
    * *예: "군사, 감시 목적으로 사용 금지" (RAIL License 등)*
    * **Risk:** 원작자가 라이선스 정책을 변경하거나 폐쇄할 경우, 해당 모델을 사용하는 서비스 전체가 법적 위험에 노출됩니다.
* **치명적 리스크 2: 파멸적 망각 (Catastrophic Forgetting)**
    * 한국어를 억지로 주입하는 과정에서, 원본 모델이 가진 고유의 논리력(Reasoning)이나 코딩 능력, 영어 능력이 훼손되는 현상이 빈번합니다.

### 3. 대표 사례
* **SKT A.X 4.0:** Qwen 2.5 기반 CPT (한국어 대량 학습)
* **KoAlpaca / Ko-Llama 류:** Llama 아키텍처 기반의 SFT 모델들
* **다수의 사내 구축형(On-Premise) LLM:** 보안을 위해 오픈소스를 가져와 사내 데이터로 튜닝한 케이스

---

## T3. 확장 모델 (Expanded Model / DUS)
**"남의 자재로 건물을 증축(Remodeling)하는 단계"**

### 1. 기술적 정의 (Technical Methodology)
단순한 튜닝을 넘어, 모델의 구조(Architecture)를 물리적으로 변형하거나 여러 모델을 결합하여 성능을 극대화한 형태입니다.

* **모델 병합 (Model Merging):**
    * 서로 다른 장점을 가진 모델(예: 수학 잘하는 모델 + 코딩 잘하는 모델)의 가중치를 수학적 기법(SLERP, TIES, DARE 등)으로 섞어서 새로운 모델을 만듭니다.
* **DUS (Depth Up-Scaling):**
    * 업스테이지 Solar v1이 채택한 방식으로, 모델의 레이어(Layer)를 복사하여 층수를 늘리는 기술입니다.
    * *예: Llama 2 (32 Layers) → 중간 16개 레이어 복제 → 48 Layers 모델 생성 + 연결 부위 추가 학습(Continued Pre-training)*
    * 처음부터 48층을 쌓는 것보다 훨씬 적은 비용으로 고성능 모델을 만들 수 있습니다.

### 2. 소버린 관점의 분석 (Sovereign Analysis)
* **주권 수준:** 🔸 **Medium (중)** - 파라미터에 대한 소유권 강화.
* **기술적 가치:**
    * 단순 튜닝(T2)보다 훨씬 고도화된 **'아키텍처 엔지니어링(Architecture Engineering)'** 기술이 들어갑니다.
    * 원본 모델(7B 등)의 한계를 넘어 더 큰 용량(10B, 11B 등)의 모델을 만들어낼 수 있습니다.
* **한계점 (The Remodeling Trap):**
    * 리모델링을 아무리 잘해도 '기초 공사(Base Architecture)'와 '자재(Pre-trained Weights)'는 남의 것을 썼다는 사실이 변하지 않습니다.
    * 원본 모델의 잠재력(Potential) 이상으로 성능을 끌어올리는 데는 한계가 존재합니다.

### 3. 판별 기준 (Checklist)
* [ ] **T2 판별:** `config.json`의 아키텍처 설정이 원본(Llama, Mistral 등)과 100% 동일한가?
* [ ] **T3 판별:** 모델 설명(Model Card)에 "Merge", "DUS", "Passthrough" 등의 병합/확장 기법이 명시되어 있는가?
* [ ] **공통:** 모델 실행 시 원작자의 라이선스(License) 고지 의무가 있는가?
