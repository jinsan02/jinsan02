## 노진산 (Jinsan Roh)

📄 **[포트폴리오](https://safe-night-557.notion.site/3cff066a406780549f81e6ff393adaa5)** · 한신대학교 컴퓨터공학부 (2027.02 졸업 예정)

**한국어 토큰을 30% 줄였더니 모델은 오히려 나빠졌습니다. 왜 그런지 찾고 있습니다.**

Qwen2.5-0.5B의 어휘 3만 개를 한국어 토큰으로 바꿨습니다. 같은 원문의 토큰 수는 30.2% 줄었지만, 같은 예산으로 CPT를 한 뒤 한국어 BPB는 37.8% 나빠졌습니다. 토큰이 줄어든 것과 모델이 좋아진 것은 따로 따져야 했습니다.

코퍼스 정제, tokenizer·embedding surgery, CPT, 평가를 RTX 5070 Ti 한 장에서 직접 했습니다. 실패한 run도 지우지 않고 결과표의 숫자마다 설정과 로그를 연결해 두었습니다.

다음에 확인할 것: 회복률이 65% 근처에서 멈추는 이유가 `tie_word_embeddings` 때문인지, untied 대조군을 두고 확인합니다.

### 대표 작업

#### [KoTokenLab](https://github.com/jinsan02/kotokenlab) — 한국어 Tokenizer Surgery & Controlled CPT

"한국어 토큰을 줄이면서 학습 후 품질도 지킬 수 있을까?"에서 시작한 개인 연구입니다.

- 원본(C0)·제거만(T2a)·치환(T2b) 세 조건을 같은 데이터와 같은 학습 일정으로 비교했습니다.
- 토크나이저가 바뀌면 PPL로는 비교가 성립하지 않아 원문 바이트 기준 BPB로 판정했고, 조건별 노이즈 플로어의 2σ를 구별 기준으로 먼저 정했습니다.
- 노름 보정과 Embedding Alignment 가설은 실험으로 반증했습니다. 새 토큰 노출을 4.4배 늘려도 회복률은 65.4%에서 65.9%로 거의 그대로였습니다.
- 근거: [`results_provenance.md`](https://github.com/jinsan02/kotokenlab/blob/main/docs/results_provenance.md)

#### [AI Agent 행동 예측](https://github.com/jinsan02/2026-ai-sw-digital-competition-ai-track) — 제한된 자원에서의 팀 실험

4인 팀장으로 검증 기준과 실험 우선순위를 정하고 서버 실험과 제출을 운영했습니다. 최종 추론 파이프라인과 INT4 확장·적용을 맡았습니다.

- 1GB 패키지와 10분 추론 제약에서 **HyperCLOVA X 0.5B** 3개를 앙상블해 팀 Macro-F1을 **0.4358 → 0.7977**로 올렸습니다.
- 0.002 미만의 Public 점수 변화는 증거로 보지 않는 기준을 세우고, 이 기준으로 기각 축 12개를 제출 전에 닫았습니다.
- 예선 8위로 본선에 진출했고, 대회를 최종 **9위/269팀**으로 마쳤으며 AI부문 후원기업상(팀스파르타 상)을 받았습니다.

#### [Qwen LLMOps](https://github.com/jinsan02/qwen-llmops) — 평가 데이터에서 모델 선택과 Serving까지

소형 언어모델을 고르는 기준부터 배포 구조까지 한 흐름으로 연결한 개인 프로젝트입니다.

- 전량 합성 1,000개 평가셋과 평가 하니스를 만들고 Q4·Q5 모델을 비교했습니다.
- Q5_K_M raw 기준 grounded **0.985**, strict **0.966**을 확인했습니다. 같은 데이터로 프롬프트를 조정했기 때문에 held-out이 아닌 in-distribution 평가로 적었습니다.
- FastAPI·Redis·ARM64 이미지와 모니터링을 구현했습니다.

### 다른 작업

- **[AI Door](https://github.com/jinsan02/2026_Korea_Japan_Bridge_ideathon)** — 고령자용 한·일 공공문서 안내 웹. 2박 3일 만에 [공개 URL](https://2026-korea-japan-bridge-ideathon.vercel.app)로 배포했고, 근거 없는 날짜·금액·연락처를 걸러내는 서버 안전 규칙 13종을 넣었습니다. 2026 한일 브릿지 아이디어톤 최우수상
- **[LG AIMERS 9기](https://github.com/jinsan02/lg-aimers-9-hackathon)** — 투구 제구 성공 확률 예측. 누적 컬럼이 시즌마다 초기화되지 않는 통산값임을 찾아 차분한 것이 단일 최대 개선(+72.64)이었습니다. 상위 19.5%(212위/1,090팀)
- **[LG AIMERS 8기](https://github.com/jinsan02/LG_Aimers_2026)** — EXAONE 4.0 1.2B calibration 데이터와 FP8·AWQ·GPTQ 비교, 최종 상위 19%
- **[SafeWave](https://github.com/jinsan02/safewave-ai-ambient-monitoring)** — WiFi CSI·음향 기반 멀티모달 Edge AI 시스템. 관련 논문으로 한국디지털콘텐츠학회 대학생 논문경진대회 동상(공저)

### 이렇게 일합니다

- 비교 전에 데이터, 학습 조건, 판정 지표를 먼저 고정합니다.
- 한 번에 한 변수만 바꿉니다.
- 팀에서는 진행 상황과 판단 근거를 문서로 공유하고, 제안과 리뷰를 다음 실험에 반영합니다.
- Claude Code와 Codex는 탐색과 구현에 활용합니다. 수치는 코드·테스트·로그·원본 파일로 다시 확인합니다.

### 기술

`Python` `PyTorch` `Transformers` `CUDA` `Linux` `Docker` `GitHub Actions` `FastAPI` `Redis Streams` `TypeScript`
