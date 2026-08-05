# GainMesh

[English](README.md) · **한국어**

**macOS 다중 출력 오디오 라우팅과 파라메트릭 EQ.**

시스템 오디오 한 줄기를 여러 스피커로 동시에 보내고, 기기별 볼륨·밸런스·지연을 따로 맞춥니다. 최대 12밴드 파라메트릭 EQ와 27개 실측 커브 프리셋을 네이티브 메뉴 막대 앱에서 제공합니다.

[![Download](https://img.shields.io/badge/download-DMG%20v1.1.2-0A84FF?style=flat-square)](../../releases/latest)
[![Platform: macOS 14.2+](https://img.shields.io/badge/platform-macOS%2014.2%2B-1D1D1F?style=flat-square)](../../releases/latest)
[![Apple silicon](https://img.shields.io/badge/chip-Apple%20silicon-635BFF?style=flat-square)](../../releases/latest)
[![License: Personal Use](https://img.shields.io/badge/license-Personal%20Use-E84D3D?style=flat-square)](LICENSE)

## 요구 사항

| | |
|---|---|
| macOS | 14.2 (Sonoma) 이상 |
| 칩 | Apple silicon (M 시리즈) |
| 권한 | 시스템 오디오 녹음 |
| 관리자 권한 | 설치 시 1회 필요 |
| 재시작 | 설치 후 1회 필요 |

## 설치

1. **[`GainMesh.dmg` 다운로드](../../releases/latest)** 후 엽니다.
2. 디스크 이미지 안의 **`Install GainMesh.pkg`** 를 실행합니다.
3. macOS가 요청하는 관리자 권한을 승인합니다.
4. 설치가 끝나면 **Mac을 재시작**합니다.
5. 재시작 후 `/Applications`에서 **GainMesh**를 실행합니다.
6. **시스템 오디오 녹음** 권한을 승인하고 출력 스피커를 선택합니다.

이 DMG는 앱을 Applications로 끌어다 놓는 설치를 제공하지 않습니다. 통합 설치 프로그램이 두 구성 요소를 함께 설치합니다.

| 구성 요소 | 설치 위치 |
|---|---|
| `GainMesh.app` | `/Applications` |
| `GainMeshDriver.driver` (서명된 HAL 플러그인) | `/Library/Audio/Plug-Ins/HAL` |

**재시작은 선택이 아닙니다.** Core Audio는 새로 설치된 HAL 드라이버를 전체 재시작에서만 읽습니다. 로그아웃이나 `coreaudiod` 재시작으로는 로드되지 않으며, 재시작 전까지는 다중 출력 라우팅이 동작하지 않습니다.

앱과 설치 프로그램은 Apple Developer ID(팀 `8YKYNYSV6L`)로 서명되고 Apple 공증을 받았습니다. Gatekeeper가 정상적으로 열어 주므로 우클릭 열기 같은 우회 절차가 필요 없습니다.

## 첫 실행

GainMesh는 메뉴 막대에서 동작합니다. Dock 아이콘과 별도 메인 창이 없습니다.

1. 메뉴 막대의 GainMesh 아이콘을 클릭합니다.
2. macOS가 묻는 **시스템 오디오 녹음** 권한을 승인합니다. 이 권한이 없으면 시스템 오디오를 가져올 수 없습니다.
3. 소리를 보낼 실제 출력 기기를 선택합니다.
4. 마스터 볼륨을 정한 뒤 기기별 볼륨·밸런스·지연을 조정합니다.
5. 이퀄라이저에서 파라메트릭 밴드, A–D 청음 슬롯, 프리셋 목록을 사용합니다.

권한 요청 창은 한 번만 나타납니다. 닫아버렸다면 **시스템 설정 → 개인정보 보호 및 보안 → 시스템 오디오 녹음**에서 GainMesh를 켠 뒤 앱을 다시 실행하세요.

**GainMesh는 로그인 시 자동으로 실행됩니다.** 설치 프로그램이 이를 미리 설정하므로, 설치 후 재시작하면 GainMesh가 이미 실행된 상태로 올라옵니다. 설정에서 끌 수 있지만, `GainMesh` 기기가 시스템 출력으로 선택된 상태에서는 앱이 실행 중일 때만 소리가 납니다.

맨 처음 실행은 Mac이 이미 쓰고 있던 스피커로 시작합니다. 아무것도 고르기 전에도 소리가 계속 납니다.

## 제거

같은 `GainMesh.dmg`를 열고 **`Uninstall GainMesh.command`** 를 실행하세요. 앱 종료, 로그인 항목 해제, 앱과 HAL 드라이버 삭제, 설정 정리까지 한 번에 처리합니다. 관리자 권한은 한 번만 승인하면 됩니다.

제거 후 Mac을 재시작해야 Core Audio가 드라이버를 놓고 원래 출력 선택으로 돌아갑니다.

앱을 휴지통에 넣는 것만으로는 부족합니다. 드라이버는 `/Library/Audio/Plug-Ins/HAL`에 있고 삭제에 관리자 권한이 필요합니다.

디스크 이미지의 항목은 설치된 앱 안의 제거 프로그램으로 향하는 링크라, GainMesh가 설치돼 있어야 동작합니다. `GainMesh.app/Contents/Resources/uninstall.command`를 직접 실행해도 됩니다.

## 문제 해결

**설치 후 소리가 안 납니다.** 아직 재시작하지 않은 경우입니다. macOS를 재시작한 뒤 GainMesh를 다시 실행하세요.

**사운드 설정에 GainMesh 출력이 보이지 않습니다.** HAL 드라이버가 로드되지 않은 상태입니다. `/Library/Audio/Plug-Ins/HAL/GainMeshDriver.driver`가 있는지 확인하고 Mac을 재시작하세요.

**"손상되었다"는 경고가 뜨거나 Gatekeeper가 열지 않습니다.** 다운로드가 중간에 끊겼거나 파일이 변조된 경우입니다. [Releases](../../releases/latest)에서 DMG를 다시 받으세요. 제3자 미러본은 사용하지 마세요.

**볼륨 키가 GainMesh를 따라가지 않습니다.** **시스템 설정 → 사운드 → 출력**에서 `GainMesh` 기기를 시스템 출력으로 선택하세요.

**기기를 바꿀 때 소리가 끊깁니다.** Core Audio가 통합 출력을 다시 구성하는 동안 잠시 기다리세요. 새 기기를 사용할 수 없으면 GainMesh가 이전 선택으로 되돌립니다.

## 언어

GainMesh는 macOS 시스템 언어를 따라 12개 언어(한국어, 영어, 일본어, 중국어 간체·번체, 프랑스어, 독일어, 스페인어, 이탈리아어, 포르투갈어(브라질), 러시아어, 아랍어)를 지원합니다. 설정에서 수동 선택할 수 있고, 목록에 없는 언어는 영어로 표시됩니다.

## 라이선스

개인·비상업적 사용은 무료입니다. 상업적 사용은 별도 허가가 필요합니다. [LICENSE](LICENSE)를 확인하세요.

Copyright © ezBuilder

---

이 저장소는 서명·공증된 배포본만 제공합니다. [소스 코드](https://github.com/ezBuilder/GainMesh)
