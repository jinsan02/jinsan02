## 노진산 (Jinsan Roh)

한국어 Foundation Model의 tokenizer·어휘 구성과 Continued Pre-training을 통제 실험으로 다룹니다.
단일 RTX 5070 Ti 16GB에서 코퍼스 정제부터 CPT, 평가, 근거 기록까지 직접 수행합니다.

데이터 고정 → 판정 지표 정의 → 노이즈 플로어 측정 → 통제 실험 → 근거 기록 순서로 일합니다.

### 주요 저장소

| 저장소 | 내용 |
| --- | --- |
| **[kotokenlab](https://github.com/jinsan02/kotokenlab)** | Qwen2.5-0.5B의 한국어 어휘 3만 개 치환 + 통제 CPT. 토큰 수 −30.2%, 한국어 BPB는 37.8% 악화. 압축 효율과 학습 후 품질의 상충을 실측 |
| **[2026-ai-sw-digital-competition-ai-track](https://github.com/jinsan02/2026-ai-sw-digital-competition-ai-track)** | AI 에이전트 행동 14-class 예측. 1GB·10분 제약에서 Macro-F1 0.4358 → 0.7977. 4인 팀장 |
| **[qwen-llmops](https://github.com/jinsan02/qwen-llmops)** | 소형 언어모델 평가 하니스·골든셋·양자화·FastAPI 배포 |
| **[LG_Aimers_2026](https://github.com/jinsan02/LG_Aimers_2026)** | EXAONE 4.0 1.2B의 domain calibration과 FP8·AWQ·GPTQ 비교 |
| **[safewave-ai-ambient-monitoring](https://github.com/jinsan02/safewave-ai-ambient-monitoring)** | WiFi CSI·음향 기반 멀티모달 Edge AI 시스템 |

### 기록 방식

- 실험은 append-only 원장(`experiments/LEDGER.tsv`)에 **성공한 run과 실패한 run을 함께** 남깁니다.
- 커밋에 `Run-Id` · `Config-SHA256` · `Invalidates` 트레일러를 붙입니다. 규약은 [`docs/COMMIT_CONVENTION.md`](https://github.com/jinsan02/kotokenlab/blob/main/docs/COMMIT_CONVENTION.md)에 있습니다.
- 예측이 빗나가면 결과를 고치지 않고 **왜 빗나갔는지**를 적습니다.
- 측정하지 않은 것은 측정하지 않았다고 적습니다.

### 도구

`Python` `PyTorch` `Transformers` `CUDA` `Linux` `Docker` `GitHub Actions` `FastAPI` `Redis Streams`

Claude Code와 Codex는 탐색과 구현에 사용하되, 실험 설계와 수치 판정, 최종 검증은 직접 합니다.
AI가 한 일을 제가 설명하지 못하면 그 결과는 제 것이 아니라고 봅니다.
