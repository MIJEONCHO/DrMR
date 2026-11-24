# Dr.MR v1 · Windows 로컬 배포 후보

ZIP 전체를 새 폴더에 풀고 `DrMR.exe`를 실행합니다. `_internal`은 같은 폴더에 두세요. 쓰기 가능한 폴더를 사용하면 GUI 결과가 기본적으로 `runs`에 저장됩니다.

## 사용 방법

- **Dr.MR**에서 확인할 Python 파일과 검증 명세를 고르고 사전 점검을 실행합니다. 사전 점검은 프로그램을 실행하지 않으므로 대상 동작 판정은 UNKNOWN입니다.
- **캡슐 스캐너**에서는 신뢰하는 합성 프로그램만 선택하고 실제 실행을 승인합니다. 결과에서 실행 상태와 대상 PASS/FAIL/UNKNOWN을 따로 읽습니다. `report/SUMMARY.html`에서 상세 보고서로 이동할 수 있습니다.
- **TARGETPROBE**에는 대상 프로그램과 명세를 같이 지정합니다. Multi-Point 예제는 `_internal/examples/synthetic_target.py` 및 `probe_spec_multipoint.json`입니다. 관련 정책과 데이터 파일은 그 폴더에 둡니다.

PowerShell에서 쓸 수 있는 예제입니다.

```powershell
.\DrMR.exe --cli check --workspace _internal\examples --program _internal\examples\invoice_bug.py --spec _internal\examples\capture.json
.\DrMR.exe --cli capture --workspace _internal\examples --program _internal\examples\invoice_bug.py --spec _internal\examples\capture.json --output runs --approve-execution
.\DrMR.exe --probe --program _internal\examples\synthetic_target.py --spec _internal\examples\probe_spec_multipoint.json --output probe-run --approve-execution
.\DrMR.exe --coverage <기존-합성-journal> <필수-경계-spec.json> <새-보고서-폴더>
```

송장 예제의 대상 FAIL은 의도한 결과입니다. P0-1 필수 경계 대조는 명세를 제공한 오프라인 세션에 적용됩니다. TARGETPROBE의 A/B/C 상태를 P0-1 관측으로 대체하거나 두 도구의 PASS를 자동 합산하지 않습니다.

## 범위와 주의사항

v1에는 Kimi GUI·Multi-Point, 기존 Doctor X 0.1.0-beta3 엔진과 A/B/C 보고서, P0-1 등록 경계 점검이 들어 있습니다. v2 후보인 미등록 경계 자동 발견, 닥터 MR 내부 관측 자동 연결, 완전한 DATA 계보, 홀로그램과 교육판은 보류합니다. 운영 TONY·Finder는 포함되지 않습니다. 번들의 Python 경로를 쓰므로 PATH의 Python에 의존하지 않습니다.

별도 프로세스는 OS 샌드박스가 아닙니다. 검토한 신뢰된 합성 프로그램만 실행하세요. 정밀 추적에는 현재 런타임에서 기존 기준본으로도 재현된 객체 필드·지연 표준 라이브러리 import·스레드 추적의 제한이 있습니다. 이런 실행은 완전한 검증의 근거로 쓰지 마세요.

## 라이선스와 제3자 고지

자체 코드의 공개 라이선스는 확정하지 않았습니다. 기존 평가 조건과 보안 문서, 제3자 고지는 `_internal/engine`에 있습니다. 번들 런타임의 PSF 고지와 PyInstaller·Tcl/Tk 고지는 `NOTICES` 및 `_internal/runtime`을 확인하세요. 이 파일은 로컬 평가 배포 후보이며 외부 공개 판단은 별도입니다.
