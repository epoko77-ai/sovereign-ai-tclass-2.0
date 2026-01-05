# 🇰🇷 한국 AI 모델 T-Class 분류 현황 (KR Models Registry)
> **Community-Driven Classification of Korean AI Models**

이 문서는 T-Class 2.0 기준에 따른 국내 주요 AI 모델의 등급 분류 현황입니다.
*이 분류는 커뮤니티의 제보와 기술적 분석을 바탕으로 하며, 각 사의 공식 입장과는 다를 수 있습니다.*

## 🏆 주요 모델 등급 현황

| 제조사 | 모델명 | 등급 | 판정 근거 (Key Factor) | 비고 (Status) |
| :--- | :--- | :---: | :--- | :--- |
| **LG** | **EXAONE-4.0-32B** | **T5** | **Architecting**(독자 연산 그래프) + **Code Independent** | **기술 주권 및 원천 IP 확보** |
| **Naver** | **HyperCLOVA X THINK** | **T5** | **Native Arch**(Peri-LN, μP) + **RLVR** + 독자 토크나이저 | **독자 설계 기반의 고도화된 추론(Reasoning) 모델** |
| **SKT** | **A.X 3.1** | **T4-2** | **From Scratch**(원천 학습) + **Scaler**(34B 독자 규격) | **자체 학습 소버린 AI (Llama 호환)** |
| **Upstage** | **Solar Pro 2** | **T4-2** | Llama 아키텍처 기반의 고도화된 스케일링(DUS) | **글로벌 호환성 및 효율 극대화** |
| **SKT** | **A.X 4.0** | **T2** | Qwen 2.5 기반 CPT (한국어/통신 데이터 추가 학습) | **오픈소스 기반 도메인 확장형** |
| **WorksAI** | WorksAI | **T0** | 빅테크 API 연동 래핑 서비스 | **자체 엔진 부재 (단순 연동)** |

> ※ **SKT A.X 3.1**은 아키텍처는 글로벌 표준(Llama)을 따르되, 34B라는 독자적 규모로 재설계(Scaling)하여 원천 학습한 **T4-2** 등급입니다.

---
### ➕ 모델 추가/수정 요청 방법
새로운 모델을 등록하거나 등급 수정을 원하시면, `Issues` 탭에 근거 자료(기술 블로그, 논문 등)와 함께 제보해 주십시오.
