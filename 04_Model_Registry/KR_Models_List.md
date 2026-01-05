# 🇰🇷 한국 AI 모델 T-Class 분류 현황 (KR Models Registry)
> **Community-Driven Classification of Korean AI Models**

이 문서는 T-Class 2.0 기준에 따른 국내 주요 AI 모델의 등급 분류 현황입니다.
*이 분류는 커뮤니티의 제보와 기술적 분석을 바탕으로 하며, 각 사의 공식 입장과는 다를 수 있습니다.*

## 🏆 주요 모델 등급 현황

| 제조사 | 모델명 | 추정 등급 | 판정 근거 (Key Factor) | 비고 |
| :--- | :--- | :---: | :--- | :--- |
| **LG** | **EXAONE-4.0-32B** | **T5** | **Architecting**(독자 연산 그래프) + **Code Independent**(전용 클래스) | **T-Class 2.0 Reference** |
| **Naver** | **HyperCLOVA X THINK** | **T5** | **Native Arch**(Peri-LN, μP) + **RLVR**(추론 강화) + 독자 토크나이저 | Sovereign AI (Reasoning) |
| **Upstage** | **Solar Pro 2** | **T4-2** | Llama 아키텍처 기반의 고도화된 스케일링 및 구조 최적화 | Global Leaderboard 상위 |
| **SKT** | **A.X 4.0** | **T2** | Qwen 2.5 기반 CPT (한국어 추가 학습) | 통신 특화 데이터 강화 |
| **WorksAI** | WorksAI | **T0** | 빅테크 API 연동 래핑 서비스 | 기업용 생산성 도구 |

> ※ 이번 **'독자 파운데이션 모델'**은 현재 평가가 진행 중이므로, 공정성을 위해 본 리스트에서 제외하였습니다.

---
### ➕ 모델 추가/수정 요청 방법
새로운 모델을 등록하거나 등급 수정을 원하시면, `Issues` 탭에 근거 자료(기술 블로그, 논문 등)와 함께 제보해 주십시오.
