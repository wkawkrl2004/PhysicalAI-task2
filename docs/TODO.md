# 해야 할 일 (TODO)

진행하면서 체크하세요. `→` 뒤는 결과물입니다.

## 1주차: 환경 · 측정 · 보정
**마일스톤: 메타 뷰에서 클릭한 위치로 팔이 이동 (오차 1cm 이하)**

### Phase A. 환경
- [ ] A1. Dofbot OS 설치, 부팅 비프음 확인
- [ ] A2. VNC 접속 → 조별 핫스팟으로 전환
- [ ] A3. Samba 설정 (PC에서 `/home/dofbot` 접근)
- [ ] A4. Docker 안 Jupyter 실행 (포트 9999)
- [ ] A5. 조이스틱 조작 확인
- [ ] A6. 카메라 2대를 Docker 안에서 동시에 인식 → `notebooks/01_camera_check.ipynb`

### Phase B. 작업장
- [ ] B1. 23cm 호, 색종이 위치 테이프로 고정
- [ ] B2. 메타 뷰 카메라 지지대 설치·고정 (작업 영역 + 색종이 3장이 화면에)
- [ ] B3. 빈 작업장 기준 사진 → `calib/ref_empty.jpg`

### Phase C. 로봇 측정 → `config/robot.json`
- [ ] C1. 관절별 최소/최대 각도
- [ ] C2. 서보 방향(SIGN)과 90° 영점 확인
- [ ] C3. 링크 길이 h, a2, a3, a4
- [ ] C4. 그리퍼 열림/닫힘/물체별 값
- [ ] C5. HOME, DROP_PAPER/VINYL/PLASTIC 자세
- [ ] C6. 자세 간 이동 충돌 확인

### Phase D. 보정 → `config/calib.json`, `config/homography.npy`
- [ ] D1. 호모그래피 (표시 6~9개)
- [ ] D2. FK/IK 구현 + 실측 15~25점으로 OFFSET 보정
- [ ] D3. 검증 10점, 평균 오차 1cm 이하 확인

## 2주차: 기본 시스템
**마일스톤: 스크립트 집기로 6개 분리수거 완료**

### Phase E. 인식
- [ ] E1. 다양한 물체 수집 (다른 조 물체 포함)
- [ ] E2. 메타 뷰 이미지 400~800장 촬영 → `data/yolo/`
- [ ] E3. 라벨링 (paper/vinyl/plastic)
- [ ] E4. YOLO 학습 (Colab) → `models/yolo.pt`
- [ ] E5. 라즈베리파이 추론 속도·정확도 확인 (처음 보는 물체 95% 이상)

### Phase F1 · G · H. 기본 동작
- [ ] F1. 접근 → 비주얼 서보잉 → 집기 스크립트
- [ ] G. DROP 자세에서 놓기
- [ ] H. 상태 머신 통합 → `notebooks/07_run_task.ipynb`
- [ ] H-test. 6개 물체 전체 실행 성공

## 3주차: 모방학습
**마일스톤: BC 정책이 스크립트 집기를 대체**

- [ ] F2-1. 데이터 수집 코드 확장 (카메라 2대, 5~10 FPS, 에피소드 단위) → `notebooks/05_collect_episodes.ipynb`
- [ ] F2-2. 클래스별 50~100 에피소드 수집
- [ ] F2-3. BC(ResNet18+MLP) 학습 스크립트 작성·학습
- [ ] F2-4. 라즈베리파이(또는 노트북) 추론 + 안전장치
- [ ] F2-5. 실패 상황 DAgger 데이터 추가 → 재학습
- [ ] F2-6. (선택) ACT로 교체

## 4주차: 강화학습 · 평가
**마일스톤: 시험 대비 완료**

- [ ] F3-1. 집기 성공 자동 판정 + 자동 리셋 구현 → `notebooks/06_rl_grasp.ipynb`
- [ ] F3-2. 클래스별 CEM/밴딧으로 집기 파라미터 최적화
- [ ] I-1. Test 1 재현 10회 (정확도·시간·실패 원인 기록)
- [ ] I-2. Test 2 재현 10회 (다른 조 물체)
- [ ] I-3. 실패 원인별 개선
- [ ] I-4. 시험 당일 체크리스트 준비 (`docs/PIPELINE.md` Phase I)

## 역할 분담 (예시)
| 담당 | 범위 |
|---|---|
| 인식 | Phase E |
| 기구학·보정 | Phase C, D |
| 학습 | Phase F2, F3 |
| 통합·테스트 | Phase G, H, I |
