# GainMesh 변경 내역 / Changelog

## 1.3.16 — 2026-08-10

### 화면 녹화 / Screen recording

- GainMesh 자체 오디오 드라이버에 시스템 출력→입력 녹음 경로를 추가했습니다.
- macOS 화면 녹화가 시스템 소리를 함께 저장하며 BlackHole이 필요 없습니다.
- 입력·출력 장치 이름을 GainMesh로 통일하고 의미 없는 Data Source Item 항목을 제거했습니다.

### 메뉴 막대와 노치 / Menu bar and notch

- 33가지 오디오 비주얼라이저 스타일과 색상 선택을 제공합니다.
- 실제 MacBook 노치의 접힌 화면에서도 펼친 비주얼의 밀도와 형태를 유지합니다.
- 펼친 화면에 비주얼 설정과 핀 토글을 메뉴 막대 크기로 배치했습니다.
- 핀 고정 상태의 그림자와 마우스 진입·이탈 동작을 안정화했습니다.
- 노치 없는 Mac에서는 가짜 노치를 제거하고 실제 메뉴 막대 위에 비주얼을 표시합니다.

### 현재 재생 중 / Now Playing

- 곡 변경 감지를 개선해 앨범 이미지·곡명·재생 상태가 빠르게 갱신됩니다.
- 앨범 영역에서 비주얼 설정을 바로 열 수 있습니다.

### 배포 품질 / Release quality

- 앱과 HAL 드라이버를 Developer ID로 서명했습니다.
- PKG와 DMG를 Apple 공증하고 스테이플했습니다.
- 전체 339개 테스트와 보안·설치 패키지 검증을 통과했습니다.

---

### English summary

- GainMesh now records system audio in macOS screen recordings without BlackHole.
- Added 33 audio visualizer styles with direct menu-bar controls.
- Improved track-change updates, compact notch rendering, pinning, shadows, and icon sizing.
- Notchless Macs now show a true menu-bar visualizer instead of a synthetic notch.
- Unified the audio input/output name as GainMesh and removed placeholder data-source items.
- Signed, notarized, and stapled PKG and DMG; 339 tests passed.
