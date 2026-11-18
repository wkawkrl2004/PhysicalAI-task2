# PhysicalAI-task2
피지컬AI실습 분리수거 과제 저장용

Dofbot + 카메라 2대(손목 카메라, 메타 뷰)로 종이·비닐·플라스틱을 분리수거하는 과제입니다.

## 파이프라인 요약
1. **인식**: 메타 뷰 → YOLO 검출 → 클래스 + 픽셀 좌표 → 호모그래피로 책상 좌표(cm)
2. **접근**: IK(+실측 보정)로 물체 위 접근 자세
3. **집기**: 손목 카메라 기반 BC/ACT 정책 (집기 파라미터는 RL로 최적화)
4. **놓기**: 클래스별 고정 자세 → 색종이 위에서 그리퍼 열기
5. 남은 물체가 없거나 제한 시간(6분)이 될 때까지 반복

자세한 내용은 [docs/PIPELINE.md](docs/PIPELINE.md) 참고.

## 폴더 구조
```
config/      robot.json(관절 범위·자세), calib.json, homography.npy
calib/       보정용 이미지와 기록
data/        yolo/(검출 데이터셋), episodes/(모방학습 에피소드) — git 제외
models/      학습된 모델 — git 제외
notebooks/   01_camera_check ~ 07_run_task
docs/        설계 문서
```
