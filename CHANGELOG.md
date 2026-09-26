# GainMesh 변경 내역 / Changelog

## 1.3.17 — 2026-09-26

**안정성**
- macOS 오디오 시스템(`coreaudiod`)이 재시작되면 스피커가 완전히 무음이 되고 앱을 다시 실행해야 했던 문제를 고쳤습니다. 이제 재시작·오디오 엔진 소실·콜백 정지를 감지해 자동으로 다시 연결합니다(유한 재시도, 사용자가 정지한 경우는 복구하지 않음).
- 재시작·충돌 후 앱을 종료하거나 정지하면 시스템 출력이 가상 GainMesh 장치에 남아 무음이 지속되던 문제를 고쳤습니다. 이제 항상 실제 스피커로 되돌립니다.
- 이미 사라진 오디오 객체 때문에 엔진이 다시 시작되지 못하던 문제를 고쳤습니다.
- 새 macOS 빌드 도구 환경에서 번역을 찾지 못해 영어로 표시될 수 있던 문제를 고쳤습니다.

**성능 (CPU 절감)**
- EQ를 스피커 채널마다 반복 계산하지 않고 원본에서 한 번만 계산합니다. 스피커 4대 기준 오디오 처리 비용이 약 3분의 1로 줄었습니다. 사용하지 않는 EQ 밴드는 계산을 건너뜁니다(출력은 비트 단위로 동일).
- 곡 정보 조회를 2–5초마다 프로세스를 새로 띄우던 방식에서, 상주 도우미가 변경 시에만 알려주는 방식으로 바꿨습니다.
- 무음일 때 노치 비주얼라이저 화면 갱신을 멈추고 스펙트럼 분석 빈도를 낮춥니다.
- 노치 비주얼(특히 워터폴·매트릭스 계열) 그리기 비용을 절반 이하로 줄였습니다.

**UI/UX**
- 메뉴 막대 아이콘이 재생 중·정지·복구 중·오류 상태를 구분해 보여줍니다.
- 자동 복구 중에는 패널에 "오디오 다시 연결 중" 상태와 "지금 다시 연결" 버튼을 표시합니다(12개 언어).
- 노치 배경을 모든 상태에서 완전한 검은색으로 통일해 비주얼이 배경화면에 묻히지 않습니다.
- 펼친 노치 카드의 앨범 아트를 누르면 재생 중인 앱(없으면 Apple Music)이 열립니다.

**업데이트**
- 새 버전이 나오면 한 번 알림을 띄우고, "다운로드"를 누르면 공증된 설치 패키지를 받아 서명(팀 8YKYNYSV6L)을 확인한 뒤 macOS 설치 프로그램을 바로 엽니다. 검증에 실패하면 다운로드 페이지를 엽니다.

### English

**Stability**
- Fixed total silence after macOS restarted its audio service (`coreaudiod`); GainMesh now detects the restart, a lost engine or a stalled callback and reconnects automatically with bounded retries (a user-stopped session stays stopped).
- Quitting or stopping after a restart/crash no longer leaves system output on the virtual GainMesh device.
- Engine restarts are no longer blocked by audio objects that Core Audio already destroyed.
- Fixed translations falling back to English with newer SwiftPM toolchains.

**Performance**
- The equalizer runs once on the source instead of once per speaker channel (~3× cheaper with four speakers); identity EQ bands are skipped with bit-identical output.
- Now-playing metadata comes from one resident helper that reports only changes, instead of launching a script every 2–5 s.
- The notch visualizer parks its display link and slows spectrum sampling during silence; drawing cost is less than half.

**UI/UX**
- State-aware menu-bar icon (playing, stopped, reconnecting, attention).
- "Reconnecting audio" panel state with a "Reconnect now" action (12 languages).
- Solid black notch background in every state.
- Clicking the album art in the expanded notch opens the playing app (or Apple Music).

**Updates**
- New versions are announced once; "Download" fetches the notarized installer package, verifies its Developer ID Installer signature for team 8YKYNYSV6L and opens macOS Installer, falling back to the download page.

---

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
