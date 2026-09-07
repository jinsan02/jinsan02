## 노진산 (Jinsan Roh)

**모델을 한 번 잘 돌리는 것보다, 비교가 성립하는 실험을 만드는 데 관심이 많습니다.**

지금은 한국어 LLM의 토큰 효율과 학습 후 품질이 어떻게 맞바뀌는지 보고 있습니다. Qwen2.5-0.5B의 어휘 3만 개를 한국어 토큰으로 바꿨더니 같은 원문의 토큰 수는 30.2% 줄었지만, 동일 예산 CPT 후 한국어 BPB는 37.8% 나빠졌습니다. 예상과 반대인 결과였고, 이때부터 압축 성공과 품질 개선을 따로 보고 있습니다.

단일 RTX 5070 Ti 16GB에서 코퍼스 정제, tokenizer·embedding surgery, CPT, 평가까지 직접 이어 왔습니다. 실험 전에는 데이터·학습 스케줄·판정 지표를 먼저 고정하고, 결과는 코드·설정·로그에서 다시 찾을 수 있게 남깁니다.

### 대표 작업

#### [KoTokenLab](https://github.com/jinsan02/kotokenlab) — 한국어 Tokenizer Surgery & Controlled CPT

“한국어 토큰을 줄이면서 학습 후 품질도 유지할 수 있을까?”에서 시작한 개인 연구입니다.

- Qwen2.5-0.5B의 어휘 3만 개를 치환하고 C0 원본·T2a 제거만·T2b 치환 조건을 비교했습니다.
- 토큰 수는 **30.2% 감소**했지만 한국어 BPB는 **37.8% 악화**했습니다. 압축 성공과 품질 개선은 같은 결론이 아니었습니다.
- 성공·실패 run을 함께 보존하고, 핵심 수치를 run ID·설정 해시·로그와 연결했습니다.
- 근거: [`results_provenance.md`](https://github.com/jinsan02/kotokenlab/blob/main/docs/results_provenance.md)

#### [AI Agent 행동 예측](https://github.com/jinsan02/2026-ai-sw-digital-competition-ai-track) — 제한된 자원에서의 팀 실험

4인 팀장으로 검증 기준과 실험 우선순위를 정하고 서버 실험과 제출을 운영했습니다. 최종 추론 파이프라인과 INT4 확장·적용을 맡았습니다.

- 1GB 패키지와 10분 추론 제약에서 팀 Macro-F1을 **0.4358 → 0.7977**로 개선했습니다.
- 한 번에 한 변수만 바꾸고, 작은 Public 점수 변화는 증거로 채택하지 않는 기준을 세웠습니다.
- 예선 8위로 본선에 진출했고, 대회를 최종 9위/269팀으로 마쳤으며 AI부문 후원기업상을 받았습니다.

#### [Qwen LLMOps](https://github.com/jinsan02/qwen-llmops) — 평가 데이터에서 모델 선택과 Serving까지

소형 언어모델을 고르는 기준부터 배포 구조까지 한 흐름으로 연결한 개인 프로젝트입니다.

- 전량 합성 1,000개 평가셋과 평가 하니스를 만들고 Q4·Q5 모델을 비교했습니다.
- Q5_K_M raw 기준 grounded **0.985**, strict **0.966**을 확인했습니다.
- FastAPI·Redis·ARM64 이미지와 모니터링을 구현했습니다.

### 다른 작업

- **[LG AIMERS 8기](https://github.com/jinsan02/LG_Aimers_2026)** — EXAONE 4.0 1.2B calibration 데이터와 FP8·AWQ·GPTQ 비교, 최종 상위 19%
- **[SafeWave](https://github.com/jinsan02/safewave-ai-ambient-monitoring)** — WiFi CSI·음향 기반 멀티모달 Edge AI 시스템

### 이렇게 일합니다

- 비교 전에 데이터, 학습 조건, 판정 지표를 먼저 고정합니다.
- 한 번에 한 변수를 바꾸고 실패한 run도 지우지 않습니다.
- 팀에서는 진행 상황과 판단 근거를 문서로 공유하고, 제안과 리뷰를 다음 실험에 반영합니다.
- Claude Code와 Codex는 탐색과 구현에 활용합니다. 수치는 코드·테스트·로그·원본 파일로 다시 확인합니다.

### 기술

`Python` `PyTorch` `Transformers` `CUDA` `Linux` `Docker` `GitHub Actions` `FastAPI` `Redis Streams`
