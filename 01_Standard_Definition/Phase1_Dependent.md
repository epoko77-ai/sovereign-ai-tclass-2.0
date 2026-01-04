# 🛑 제1구간: 의존 단계 (The Dependent Phase)
> **"AI를 소유하지 않고, 빌려 쓰는 단계 (Rent-a-Model)"**

이 구간은 AI 서비스(Application)를 개발하는 단계이지, AI 기술(Technology)을 보유한 단계가 아닙니다. 
빠른 시장 진입(Time-to-Market)에는 유리하지만, AI 주권이나 통제권은 공급사(Vendor)에게 완전히 종속되어 있습니다.

---

## T0. API 래퍼 (Wrapper)

### 1. 기술적 정의 (Technical Definition)
* 자체적인 추론 엔진(Inference Engine)이나 모델 가중치(Weights)를 보유하지 않습니다.
* OpenAI(GPT), Anthropic(Claude), Google(Gemini) 등의 **폐쇄형 API(Proprietary API)**를 호출하여, 그 결과를 단순히 UI로 보여주거나 프롬프트 엔지니어링을 통해 일부 맥락만 제어하는 형태입니다.

### 2. 소버린 관점의 분석 (Sovereign Analysis)
* **주권 수준:** ❌ **None (없음)**
* **데이터 통제권:** 사용자의 데이터가 프롬프트 형태로 API 공급사의 서버로 전송됩니다. '학습 데이터로 쓰지 않음' 옵션을 켜더라도, 데이터의 물리적 위치는 해외에 있습니다.
* **사업 지속성:** 공급사가 API 가격을 올리거나, 정책을 변경하여 특정 서비스(예: 성인물, 의료 조언 등)를 차단하면 즉시 서비스가 중단됩니다.

### 3. 판별 기준 (Checklist)
* [ ] 모델의 가중치 파일(safetensors, bin)을 보유하고 있는가? (No)
* [ ] 인터넷 연결 없이 로컬(On-premise)에서 구동 가능한가? (No)
* [ ] API 공급사의 서버가 다운되면 서비스도 멈추는가? (Yes)

---

## T1. 파인 튜너 (Closed-Weight Fine-Tuner)

### 1. 기술적 정의 (Technical Definition)
* Azure OpenAI Service나 AWS Bedrock 같은 PaaS형 플랫폼 위에서, 기반 모델(Base Model)의 가중치는 건드리지 못하고 **어댑터(LoRA 등) 계층만 학습**하거나 **데이터셋만 주입**하는 형태입니다.
* 모델의 핵심 뇌 구조는 여전히 공급사의 통제 하에 있는 '블랙박스(Blackbox)' 상태입니다.

### 2. 소버린 관점의 분석 (Sovereign Analysis)
* **주권 수준:** 📉 **Very Low (최하)**
* **설명 가능성(XAI) 부재:** 모델이 왜 그런 답변을 했는지 원인을 파악하려면 기반 모델의 학습 데이터를 봐야 하지만, 접근 권한이 없습니다.
* **환각(Hallucination) 수정 불가:** 잘못된 지식을 뱉어내도, 근본적인 수정을 할 수 없고 RAG(검색 증강) 같은 땜질 처방만 가능합니다.

### 3. 대표 사례 및 한계
* **UAE TAMM 3.0:** 정부 서비스를 GPT 기반으로 구축했으나, 데이터 주권 문제로 논란.
* **KT ChatGPT-4ok:** MS Azure 기반으로 보안을 강화했으나, 결국 기술의 뿌리는 MS/OpenAI에 종속.
