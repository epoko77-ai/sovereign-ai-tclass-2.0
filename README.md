# 🇰🇷 Sovereign AI T-Class 2.0 Standard
> **The Standard Framework for AI Sovereignty and Technical Independence**
> (소버린 AI 주권 등급 표준 2.0)

![License](https://img.shields.io/badge/license-CC--BY--SA%204.0-blue.svg) ![Status](https://img.shields.io/badge/status-Active-green.svg) ![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## 📖 개요 (Introduction)
최근 AI 모델의 유사성 논란과 기술 유출 공방을 보며, 우리는 소모적인 논쟁을 넘어 **"무엇이 진정한 기술 주권(Sovereignty)인가?"**에 대한 명확한 기준을 정립해야 합니다.

이 프로젝트는 글로벌 기술 트렌드와 **엔지니어링 실체(Engineering Reality)**를 반영하여, AI 모델의 주권 수준을 판별하는 **[7단계 등급 체계 (T-Class 2.0)]**를 정의합니다.

이 기준은 단순한 성능 평가가 아닙니다.
* **Data Sovereignty:** 데이터의 기원과 통제권
* **Technical Independence:** 아키텍처 및 코드의 수정 권한
* **Security:** 국가 안보적 가치와 인프라 자립도

---

## 💡 우리의 철학: OSS 현실과 생태계 전략 (Philosophy)
본 표준은 '완전한 무에서의 창조'만을 고집하지 않습니다. 현대 AI 개발의 현실과 오픈소스 생태계의 본질을 꿰뚫는 엔지니어링 관점을 지지합니다.

### 1. OSS 참조의 연속성 (The Spectrum)
개발 현장에서 오픈소스 활용은 '사용 vs 미사용'의 이분법이 아닌 연속선(Spectrum) 위에 있습니다.
* **참조(Reference):** 아이디어·논문·구조만 참고하여 새로 구현
* **재사용(Reuse):** 포크(Fork) 또는 단순 복사
* **회색 지대(Grey Zone):** 원형 코드를 가져왔으나 로직과 구조를 대폭 수정하여 판단이 모호한 영역

### 2. 개발자의 딜레마와 보수적 결정
'회색 지대'에서 엔지니어는 법률적 선을 긋기 어렵습니다. 따라서 우리는 **"애매하면 숨기기보다 명확히 표기하여 리스크를 없애는 것"**이 가장 정직하고 보수적인 엔지니어링 판단이라고 봅니다. 라이선스 표기는 도용의 자백이 아니라, 투명성을 위한 기술적 결단입니다.

### 3. 전략적 개방과 기술 주도권
우리는 다음과 같은 가치를 지향합니다.
> **"우리가 수정한 것도, 그리고 만든 것들도 Apache 등으로 오픈해서 남이 더 많이 활용하도록 해야 생태계의 일원이 되고 기술 주도권을 가져간다."**

방어를 넘어 기여를 통해 글로벌 표준을 리딩하는 것, 그것이 T-Class가 지향하는 진정한 소버린 AI의 방향입니다.

---

## 🚀 왜 T-Class 2.0인가? (Why This Matters)
기존의 '국산 AI' 논쟁은 모호했습니다. 이 기준은 **Code(설계), Weights(지능), Data(기원)**라는 3가지 실체에 기반하여 투명한 잣대를 제시합니다.

> **"Sovereign AI means a nation owns its own data and the intelligence it produces."**
> — Jensen Huang (NVIDIA CEO)

우리는 이 정의에 따라 **T4(Architecture Scaler)**를 산업적 표준으로, **T5(Native Architecture)**를 국가적 안보 목표로 제안합니다.

---

## 📊 T-Class 2.0 요약 (Summary Table)

| 구간 | 등급 | 명칭 | 핵심 특징 | 주권/통제 수준 |
| :--- | :--- | :--- | :--- | :--- |
| **제1구간**<br>(의존 단계) | **T0** | API Wrapper | 빅테크 API 호출, 껍데기만 존재 | ❌ **없음 (None)** |
| | **T1** | Fine-Tuner | 폐쇄형 모델 미세조정 (블랙박스) | 📉 **최하 (Very Low)** |
| **제2구간**<br>(과도기) | **T2** | CPT Model | 오픈소스 + 추가학습 (라이선스 종속) | 🔸 **하 (Limited)** |
| | **T3** | Expanded (DUS) | 오픈소스 병합 및 확장 (리모델링) | 🔸 **중 (Partial)** |
| **제3구간**<br>(표준 단계) | **T4** | **From Scratch** 🎖️ | **아키텍처 차용 + 가중치 자체 학습** | ✅ **통제권 확보 (Control)** |
| | *T4-1* | *Adopter* | *설정값 그대로 학습 (단순 도입)* | *Data Sovereignty* |
| | *T4-2* | *Scaler* | *구조 최적화 및 확장 (Global Standard)* | *Tech Sovereignty* |
| **제4구간**<br>(리더십) | **T5** | Native Arch 🎖️ | 독자 설계 + 한국어 토크나이저 | 🛡️ **완전 통제 (Full Control)** |
| | **T6** | Full-Stack 🎖️ | T5 + 국산 NPU + 국산 클라우드 | 👑 **국가 안보 (Security)** |

---

## 🖼️ 한눈에 보는 판별 로직 (Logic Flow)

```mermaid
graph TD
    Start[🚀 내 모델 등급 진단하기] --> Q1{Q1. 가중치를 처음부터<br>자체 학습했는가?<br>(Pre-training)}
    
    Q1 -- No --> NonSov[❌ 비 소버린 구간<br>(T0 ~ T3)]
    Q1 -- Yes --> Sov[🎖️ 소버린 구간 진입<br>(통제권 확보)]
    
    Sov --> Q2{Q2. 독자적인<br>모델링 코드를 쓰는가?<br>(Custom Code)}
    
    NonSov -.-> T2[T2/T3. 튜닝 및 확장]
    
    Q2 -- No<br>(표준호환) --> Q3{Q3. 구조 변경이나<br>최적화를 수행했는가?}
    Q2 -- Yes<br>(독자코드) --> T5[🛡️ T5. 네이티브 아키텍처]

    Q3 -- No --> T4_1[T4-1. 아키텍처 어답터]
    Q3 -- Yes --> T4_2[✅ T4-2. 아키텍처 스케일러]
    
    T5 --> Q4{Q4. 국산 인프라<br>(NPU/Cloud)인가?}
    Q4 -- Yes --> T6[👑 T6. 풀스택 소버린]

    style Sov fill:#d4edda,stroke:#28a745,stroke-width:2px,stroke-dasharray: 5 5
    style T4_2 fill:#d4edda,stroke:#28a745,stroke-width:4px
    style T5 fill:#cce5ff,stroke:#004085,stroke-width:4px
    style T6 fill:#fff3cd,stroke:#856404,stroke-width:4px
